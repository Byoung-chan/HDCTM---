# HDCTM-김창흡 한시분석도구 및 결과
### HDCTM-Kim Chang-heup's Classical Chinese Poetry Analysis Tool and Results

본 저장소는 조선 후기 대문호 삼연(三淵) 김창흡(金昌翕)의 문집인 *삼연집(三淵集)*에 수록된 한시 5,247편을 대상으로 한 하이브리드 토픽 모델링 분석 코드와 데이터셋 일체를 제공한다.

본 연구는 고전 한시와 같이 고도로 압축되고 은유적인 텍스트 환경에서 발생하는 기존 통계적 토픽 모델링의 파편화 문제를 해결하기 위해, 대형 언어 모델(LLM)을 활용한 사전 의미해석 특징 피처 추출 기법(주제·유형·정서 3축 스키마)과 밀도 기반 군집화(HDBSCAN) 알고리즘을 결합한 고밀도 압축 텍스트 토픽 모델링(HDCTM) 아키텍처를 제안하고 실증한다.

이용자의 다운로드 편의성과 대용량 파일 관리의 효율성을 위해 소스 코드를 포함한 모든 데이터셋 파일은 구글 드라이브(Google Drive)의 단일 공유 폴더를 통해 일괄 공개한다.

---

## 1. 통합 다운로드 링크 (Data & Code Access)

아래의 구글 드라이브 링크를 통해 파이썬 소스 코드, 논문 교차 검증용 원본 데이터, 단계별 분석 결과 데이터셋 전체를 일괄 다운로드할 수 있다. 공유 폴더 구조 그대로 개별 파일을 열람하거나, 전체 통합본 압축 파일을 내려받을 수 있다.

* 🔗 **구글 드라이브 공유 폴더 바로가기**
* **최상위 공유 폴더명:** `HDCTM-김창흡한시분석도구및결과`

> 💡 **원본성(날짜) 검증 안내**
> 분석 알고리즘이 구동되어 결과 파일들이 최초로 생성된 시점의 실제 타임스탬프(2026년 4월 20일 등 폴더의 속성 예외)를 그대로 복원하여 서지학적 원본성을 검증하고자 하는 연구자는, 개별 파일 다운로드 대신 최상위 디렉터리에 배치된 `01_HDCTM_김창흡한시분석_통합패키지.zip` 파일을 다운로드하여 압축을 해제하는 것을 권장한다.

---

## 2. 저장소 구조 및 세부 파일 명세 (Directory Tree & Specifications)

구글 드라이브 공유 폴더 내부의 최종 적재 구조와 각 파일의 학술적·기능적 명세는 다음과 같다.

### 2.1. 통합 디렉터리 트리 (Unified Directory Tree)

```text
HDCTM_김창흡한시분석/
├── 01_HDCTM_김창흡한시분석_통합패키지.zip # 소스 코드 및 데이터 전체를 포함한 일괄 압축 파일(데이터 투명성 검증용 원본 날짜 유지)
├── 02_하이브리드토픽모델링분석기.py       # 토픽 모델링 파이프라인 메인 파이썬 코드
├── 03_Original_Data/                       # 인문학 논문 검증용 추출 원본 데이터
│   └── 삼연시학메타주제표준화통합데이터.xlsx
│
├── 04_BottomUp_Analysis/                   # 미시 어휘 중심 상향식 자율 군집 결과
│   ├── 0439. 삼연집(三淵集)_bottomup_analysis_metadata.csv
│   ├── 0439. 삼연집(三淵集)_bottomup_meta_report.html
│   ├── step1_clustered.csv
│   ├── step2_summaries.csv
│   ├── step3_meta_clustered.csv
│   └── step4_final_reports/
│       ├── report_meta_0.json
│       ├── report_meta_1.json
│       ├── report_meta_2.json
│       ├── report_meta_3.json
│       ├── report_meta_4.json
│       ├── report_meta_5.json
│       └── report_meta_6.json
│
└── 05_TopDown_Analysis/                    # 거시 맥락 중심 하향식 병합 결과 (전수 한시 포함)
    ├── 0439. 삼연집(三淵集)_merged_all_topdown_analysis_metadata.csv
    ├── 0439. 삼연집(三淵集)_merged_all_topdown_meta_report.html
    ├── step1_summaries.csv
    ├── step2_meta_clustered.csv
    └── step3_final_reports/
        ├── report_meta_0.json
        ├── report_meta_1.json
        ├── report_meta_2.json
        └── report_meta_3.json

```

### 2.2. 파일별 세부 상세 명세 (Detailed File Specifications)

#### 📂 최상위 경로 (Root)

* **`01_HDCTM_김창흡한시분석_통합패키지.zip`**: 소스 코드 및 데이터 전체를 포함한 일괄 압축 파일이다. 연구 데이터의 신뢰성과 투명성 검증을 위해 최초 생성된 시점의 원본 파일 수정 날짜 속성을 그대로 보존하고 있다.
* **`02_하이브리드토픽모델링분석기.py`**: 대형 언어 모델(LLM)과 밀도 기반 군집화 알고리즘을 결합한 분석 파이프라인 구동용 통합 GUI 애플리케이션 소스 코드이다. 분석 초기 단계에 LLM을 가동하여 주제, 유형, 정서의 3축 키워드를 추출하고, 이를 한시 원문과 합성하여 '지식 증강형(Knowledge-Augmented) 임베딩' 공간을 구축하도록 설계되어 있다.

#### 📂 `03_Original_Data/` (논문 검증용 추출 데이터)

* **`삼연시학메타주제표준화통합데이터.xlsx`**: 데이터 기반의 하이브리드 토픽 모델링 분석 결과와 실제 인문학 논문 본문에 기술된 질적 비평 내용, 통계적 성과 수치 및 구체적인 서정 정조 사례 간의 교차 비교 검증을 위해 별도로 정제하여 확보한 원본 데이터셋이다.

#### 📂 `04_BottomUp_Analysis/` (상향식 분석 결과)

데이터 제어 자유도를 극대화하여 작품 본연의 수사 구조를 보존하고 데이터 내재적 분포망으로부터 미지의 미시 군집을 탐색적으로 도출하는 상향식(Phase 2-B) 트랙의 연산 결과물이다.

* **`0439. 삼연집(三淵集)_bottomup_analysis_metadata.csv`**: 상향식 데이터 경로를 통해 도출된 미시 군집 ID 및 개별 작품별 속성 키워드가 통합된 마스터 메타데이터 파일이다.
* **`0439. 삼연집(三淵集)_bottomup_meta_report.html`**: 데이터 주도로 도출된 7개의 독창적인 미시 메타 주제 영역과 기하학적 무게중심(Centroid) 기준 대표시 분석 결과를 웹브라우저 상에서 시각적으로 즉시 열람할 수 있도록 컴파일된 HTML 보고서이다.
* **`step1_clustered.csv` ~ `step3_meta_clustered.csv**`: 지식 증강형 벡터 공간에 기반한 초기 자율 군집화, LLM 기반 군집 요약문 생성, 요약문 벡터를 대상으로 한 최종 메타 주제 군집화까지의 단계별 중간 연산 데이터이다.
* **`step4_final_reports/`**: 설명 가능한 AI(XAI) 관점에서 기하학적 이상치(Outlier) 격리 근거 및 대표시-이웃 작품 간의 의미론적 일관성을 문헌학적으로 정성 검증할 수 있도록 지원하는 JSON 형식의 최종 리포트 분할 파일(0번~6번)들의 집합이다.

#### 📂 `05_TopDown_Analysis/` (하향식 병합 분석 결과)

데이터 제어 자유도를 최소화하여 의미론적 일관성의 붕괴를 제어하고, 규격화된 스키마 분류 템플릿에 따라 거시적 사상 정렬을 전개하는 하향식(Phase 2-A) 전문가 경로의 결과물이다. 실험 대상이 된 삼연집 한시 데이터 5,247편 전체를 완전히 내포하고 있다.

* **`0439. 삼연집(三淵集)_merged_all_topdown_analysis_metadata.csv`**: 스키마 구조화 및 대주제 수렴 정렬이 100% 완료된 하향식 통합 마스터 메타데이터 파일이다.
* **`0439. 삼연집(三淵集)_merged_all_topdown_meta_report.html`**: 문헌학적 Ground Truth(대자연 귀의와 은일 수양, 사회 현실 고발과 풍자 등 작가의 실제 역사적 삶의 궤적)와 정밀하게 부합하도록 정렬된 4대 거시 대주제의 심층 분석 내용을 수록한 HTML 보고서이다.
* **`step1_summaries.csv` / `step2_meta_clustered.csv**`: 동일 레이블 코드 조합 소그룹의 수학적 무게중심 대표작 선정, 개념 요약문 도출 및 요약문 수준 추상화 공간에서의 메타 군집화 연산이 수행된 단계별 데이터이다.
* **`step3_final_reports/`**: 하향식 전문가 가이드 통합 트랙의 최종 대주제별 심층 분석 논문 원고가 집약된 JSON 형식의 리포트 파일(0번~3번)들의 집합이다.

---

## 3. 실행 환경 및 기술 사양 (Technical Environment)

### 하드웨어 및 소프트웨어 사양

* **언어 및 시스템:** Python 3.11, PyTorch 2.1.1
* **핵심 라이브러리:** scikit-learn 1.3.0, scipy 1.11.3, hdbscan 0.8.29, umap-learn 0.5.3
* **임베딩 엔진:** Google Vertex AI text-multilingual-emb-002 (768차원 고차원 벡터 변환)
* **클라우드 API:** Gemini 1.5 Pro (Vertex AI)
* **인코딩 설정:** 인코딩 설정을 일관되게 보존하고 한글 깨짐을 방지하기 위해 모든 연산 파일은 `UTF-8-SIG` 규격을 적용함.

### 연구 활용 안내

본 데이터셋과 도구는 고전 한문학 텍스트의 통사적 한계인 희소 데이터셋(Sparse Dataset) 및 파편화 현상을 극복하기 위한 방법론적 기초 자료로 활용될 수 있다. 특히 시적 의도의 왜곡 없이 고전 시가의 미시적 감정선과 역사적 지시 대상을 계량화하는 전산인문학 연구의 실증 사례로 기능한다.

> 💡 **한시 분석 최적화 참고 사항**
> 한시는 산문과 달리 매우 단문 위주의 압축적이고 은유적인 문장 구조가 주를 이루므로, 토픽 추출 파이프라인에서 시드 길이(seed length) 임계치를 축소 조정하고 하이퍼파라미터를 세밀하게 조율하여 분석 해상도를 극대화하였습니다.

---

## 4. 연구 인용 및 참조 논문 (Citation)

본 저장소의 소스 코드 및 데이터셋을 학술 연구, 논문 작성, 혹은 2차 가공에 활용할 경우 아래의 출처를 명확히 표기해야 한다.

### 관련 연구 논문

* **논문명:** "대규모 언어 모델 기반의 고밀도 압축 텍스트 토픽 모델링 기법-고전 한시(漢詩)를 중심으로"
* **게재지:** 한국컴퓨터정보학회논문지 (Journal of The Korea Society of Computer and Information)

### 데이터셋 및 도구 인용

```bibtex
@misc{hdctm2026,
  author       = {*******},
  title        = {HDCTM-김창흡 한시분석도구 및 결과},
  year         = {2026},
  publisher    = {GitHub},
  journal      = {GitHub Repository},
  howpublished = {\url{[https://github.com/your-repository/HDCTM-Kim-Chang-Heup](https://github.com/your-repository/HDCTM-Kim-Chang-Heup)}}
}

```

---

## 5. 라이선스 (License)

* **소스 코드 (Python Script):** MIT License 적용
* **데이터셋 (Excel, CSV, JSON, HTML):** Creative Commons Attribution 4.0 International (CC-BY-4.0) 라이선스에 의거하여, 적절한 출처 표기 및 인용 하에 상업적·비상업적 재배포와 2차 저작물 작성이 자유롭게 허용된다.

```

```
