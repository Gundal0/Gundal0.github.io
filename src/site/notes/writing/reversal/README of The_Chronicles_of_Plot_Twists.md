---
{"dg-publish":true,"permalink":"/writing/reversal/readme-of-the-chronicles-of-plot-twists/","dg-note-properties":{}}
---


# 옵시디언(Obsidian) 볼트 사용 및 전자책(eBook/PDF) 출판 가이드

환영합니다! 본 디렉터리(`/Users/kimgunuk/.gemini/antigravity/scratch/plot_twists_chronicles/`)에는 출판 수준으로 집필된 전문 반전 서사 분석서인 **《반전의 연대기: 픽션과 현실을 뒤흔든 충격의 서사학 (The Chronicles of Plot Twists)》** 마크다운 원고가 포함되어 있습니다.

---

## 📂 파일 구성 안내

- **`The_Chronicles_of_Plot_Twists.md`**: 본 도서의 마스터 통합본 (단행본 1권 분량, 총 6부 24개 핵심 챕터, 서문, 작법론 매트릭스, 공식 아카이브 웹사이트 수록).
- **`README.md`**: 옵시디언 볼트 설정 및 PDF/전자책 변환 매뉴얼 (현재 파일).

---

## 🚀 옵시디언(Obsidian)에서 바로 열고 활용하기

### 1. 옵시디언 볼트(Vault)로 열기
1. **옵시디언(Obsidian)** 프로그램을 실행합니다.
2. 좌측 하단의 금고(Vault) 아이콘을 클릭하고 **[Open folder as vault (폴더를 보관함으로 열기)]** 를 선택합니다.
3. 경로 지정:
   `/Users/kimgunuk/.gemini/antigravity/scratch/plot_twists_chronicles`
4. 이제 본 마크다운 문서가 완벽한 하이퍼링크와 콜아웃이 적용된 지식 베이스로 활성화됩니다.

### 2. 추천 플러그인 (Community Plugins)
본 도서는 다음 플러그인과 연동할 때 최상의 가독성과 인터랙티브 기능을 제공합니다:
- **Dataview**: 본문 속 `Type::`, `Year::`, `TwistCategory::` 인라인 메타데이터를 기반으로 표(Table)나 목록(List)을 자동 생성합니다.
- **Advanced Tables**: 제6부의 반전 작법 매트릭스를 스프레드시트처럼 정렬하고 탐색할 수 있습니다.
- **Mermaid.js**: 내장되어 있으므로 별도 설치 없이도 서사 구조 왜곡 시퀀스 다이어그램이 자동 렌더링됩니다.

---

## 🖨️ PDF 소책자 및 전자책(ePub) 출판 방법

### 1. 옵시디언 자체 PDF 내보내기 (가장 간편함)
1. 옵시디언에서 `The_Chronicles_of_Plot_Twists.md`를 엽니다.
2. 우측 상단의 `...` (추가 옵션) 버튼을 누르고 **[Export to PDF (PDF로 내보내기)]** 를 클릭합니다.
3. 설정 옵션:
   - **Page size**: A4 또는 A5 (소책자/단행본 판형으로 A5 추천)
   - **Downscale percent**: 100%
   - **Include file name as title**: 꺼짐 (OFF)
4. 내보내기를 누르면 출판물 규격의 깔끔한 소책자 PDF가 완성됩니다.

### 2. Pandoc을 이용한 전문 ePub / PDF 변환 (고급 사용자)
터미널에서 Pandoc을 이용해 즉시 ePub 전자책으로 변환할 수 있습니다:
```bash
cd /Users/kimgunuk/.gemini/antigravity/scratch/plot_twists_chronicles
pandoc The_Chronicles_of_Plot_Twists.md -o The_Chronicles_of_Plot_Twists.epub --toc --toc-depth=2
```
