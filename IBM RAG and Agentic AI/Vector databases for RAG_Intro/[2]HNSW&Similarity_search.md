# 📘 ChromaDB: 아키텍처, HNSW 인덱싱 및 필터링 심화 가이드

ChromaDB는 단순한 데이터 저장소가 아닌, 고차원 벡터 데이터를 효율적으로 관리하고 검색하기 위한 **벡터 데이터베이스**입니다. 본 가이드는 ChromaDB의 내부 작동 원리부터 실전 검색 최적화 기법까지 다룹니다.

---

## 1. 벡터 인덱스(Vector Index)와 HNSW

### 🔍 왜 인덱스가 필요한가?
모든 벡터를 일일이 비교하는 '무차별 대입(Brute-force)' 방식은 데이터가 많아질수록 속도가 급격히 느려집니다. 이를 해결하기 위해 **벡터 인덱스**를 사용하여 검색 범위를 좁히고 지연 시간(Latency)을 단축합니다.

### 🕸️ HNSW (Hierarchical Navigable Small World)
ChromaDB가 사용하는 유일한 인덱싱 알고리즘으로, 그래프 기반의 **근사 최근접 이웃(ANN)** 검색 방식입니다.



* **다층 구조**: 상위 레이어에서 크게 건너뛰며 검색하고, 하위 레이어에서 세부적으로 정밀 탐색합니다.
* **Small World 효과**: 대부분의 노드가 몇 단계 안에 연결되어 있어 수백만 개의 데이터도 빠르게 탐색 가능합니다.
* **장점**: 고속 검색, 높은 정확도(Recall), 대규모 데이터 확장성.

---

## 2. HNSW 성능 튜닝 파라미터

컬렉션 생성 시 `configuration`을 통해 속도와 정확도 사이의 균형을 맞출 수 있습니다.

| 파라미터 | 설명 | 기본값 | 특징 |
| :--- | :--- | :--- | :--- |
| `space` | 거리 측정 방식 | `l2` | `cosine`, `ip`(내적), `l2`(유클리드) 중 선택 |
| `ef_construction` | 인덱스 구축 시 후보군 크기 | 100 | 높을수록 인덱스 품질 향상, 메모리 및 시간 증가 |
| `ef_search` | 검색 시 탐색 후보군 크기 | 100 | 높을수록 검색 정확도(Recall) 향상, 속도 저하 |
| `max_neighbors` | 각 노드의 최대 연결 수 | 16 | 높을수록 그래프가 촘촘해져 정확도 향상 |

```python
# HNSW 설정 예시
collection = client.create_collection(
    name="optimized_collection",
    configuration={
        "hnsw": {
            "space": "cosine",
            "ef_search": 100,
            "ef_construction": 100,
            "max_neighbors": 16
        }
    }
)