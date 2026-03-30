# [API Spec] ETF 분배금 추이 (SEIBro)

## Overview
한국예탁결제원(SEIBro)에서 제공하는 ETF(상장지수펀드)의 분배금 지급 현황 및 추이 정보를 제공하는 서비스입니다. 실제 네트워크 호출은 XML 기반의 POST 요청으로 이루어집니다.

## Endpoint
`https://seibro.or.kr/websquare/engine/proworks/callServletService.jsp`

## Request (InBlock_1)
XML 페이로드의 `<reqParam>` 태그 내에 속성으로 `action="exerInfoDtramtPayStatPlist"` 및 `task="ksd.safe.bip.cnts.etf.process.EtfExerInfoPTask"`가 지정되어야 합니다.

| 파라미터명 | 타입 | 설명 |
| :--- | :--- | :--- |
| fromRGT_STD_DT | string | 지급기준일 시작 (YYYYMMDD) |
| toRGT_STD_DT | string | 지급기준일 종료 (YYYYMMDD) |
| isin | string | 종목코드 (선택사항) |
| mngco_custno | string | 운용사코드 (선택사항) |
| etf_sort_cd | string | ETF 분류코드 |
| START_PAGE | string | 시작 페이지 번호 |
| END_PAGE | string | 종료 페이지 번호 |

## Response (OutBlock_1)
응답은 `<vector>` 내의 `<result>` 태그 리스트로 반환됩니다.

| 필드명 | 타입 | 설명 |
| :--- | :--- | :--- |
| ISU_CD | string | 종목코드 (ISIN 매핑) |
| ISU_NM | string | 종목명 (KOR_SECN_NM 매핑) |
| RECD_DT | string | 지급기준일 (RGT_STD_DT 매핑) |
| PYMT_DT | string | 실지급일 (TH1_PAY_TERM_BEGIN_DT 매핑) |
| DIST_AMT | string | 주당분배금 (BUNBE 매핑) |
| TAX_STD_PRC | string | 과표기준가 (TAXSTD 매핑) |
| MNG_NM | string | 운용사명 (REP_SECN_NM 매핑) |
| CAT_NM | string | ETF분류명 (ETF_SORT_NM 매핑) |
| DIST_RSN | string | 분배사유 (RGT_RSN_DTAIL_NM 매핑) |

## Samples

### Request Sample (XML)
```xml
<reqParam action="exerInfoDtramtPayStatPlist" task="ksd.safe.bip.cnts.etf.process.EtfExerInfoPTask">
    <fromRGT_STD_DT value="20250328"/>
    <toRGT_STD_DT value="20260327"/>
    <isin value=""/>
    <mngco_custno value=""/>
    <START_PAGE value="1"/>
    <END_PAGE value="30"/>
</reqParam>
```

### Response Sample (XML Extract)
```xml
<result>
    <ISIN value="KR7276970001"/>
    <KOR_SECN_NM value="KODEX 미국S&amp;P500배당귀족커버드콜(합성 H)"/>
    <RGT_STD_DT value="20260325"/>
    <TH1_PAY_TERM_BEGIN_DT value="20260327"/>
    <BUNBE value="1.50968"/>
    <TAXSTD value="9785.44"/>
    <ETF_SORT_NM value="파생상품/구조화"/>
    <REP_SECN_NM value="삼성자산운용"/>
    <RGT_RSN_DTAIL_NM value="이익분배"/>
</result>
```
