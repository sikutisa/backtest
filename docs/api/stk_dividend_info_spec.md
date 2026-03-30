# [API Spec] 기업별 배당정보 (SEIBro)

## Overview
한국예탁결제원(SEIBro)에서 제공하는 기업별 상세 배당 내역 정보를 제공하는 서비스입니다. 실제 네트워크 호출은 XML 기반의 POST 요청으로 이루어집니다.

## Endpoint
`https://seibro.or.kr/websquare/engine/proworks/callServletService.jsp`

## Request (InBlock_1)
XML 페이로드의 `<reqParam>` 태그 내에 속성으로 `action="divStatInfoPList"` 및 `task` 경로가 지정되어야 하며, 내부 파라미터는 다음과 같습니다.

| 파라미터명 | 타입 | 설명 |
| :--- | :--- | :--- |
| RGT_STD_DT_FROM | string | 배당기준일 시작 (YYYYMMDD) |
| RGT_STD_DT_TO | string | 배당기준일 종료 (YYYYMMDD) |
| ISSUCO_CUSTNO | string | 발행회사번호 (기업 식별자) |
| KOR_SECN_NM | string | 종목명 |
| SECN_KACD | string | 주식종류코드 |
| RGT_RSN_DTAIL_SORT_CD | string | 배당구분코드 |
| LIST_TPCD | string | 시장구분코드 |
| START_PAGE | string | 시작 페이지 번호 |
| END_PAGE | string | 종료 페이지 번호 |

## Response (OutBlock_1)
응답은 `<vector>` 내의 `<result>` 태그 리스트로 반환됩니다.

| 필드명 | 타입 | 설명 |
| :--- | :--- | :--- |
| RGT_STD_DT | string | 배정기준일 |
| TH1_PAY_TERM_BEGIN_DT | string | 현금배당 지급일 |
| DELI_DT | string | 주식 유통(교부)일 |
| KN_DIV_PAY_DT | string | 현물배당 지급일 |
| SHOTN_ISIN | string | 종목코드 (단축코드) |
| KOR_SECN_NM | string | 종목명 |
| LIST_TPNM | string | 시장구분 |
| RGT_RSN_DTAIL_SORT_NM | string | 배당구분 |
| SECN_DTAIL_KANM | string | 주식종류 |
| CASH_ALOC_AMT | string | 주당배당금 (일반) |
| DIFF_ALOC_AMT | string | 주당배당금 (차등) |
| CASH_ALOC_RATIO | string | 주당배당률-현금 (액면가 대비 %) |
| STK_ALOC_RATIO | string | 주식배당률 |
| ESTM_STDPRC | string | 단주기준가 |
| PVAL | string | 액면가 |
| SETACC_MM | string | 결산월 |
| AG_ORG_TPNM | string | 명의개서대리인 |

## Samples

### Request Sample (XML)
```xml
<reqParam action="divStatInfoPList" task="ksd.safe.bip.cnts.Company.process.EntrFnafInfoPTask">
    <RGT_STD_DT_FROM value="20260302"/>
    <RGT_STD_DT_TO value="20260330"/>
    <ISSUCO_CUSTNO value=""/>
    <KOR_SECN_NM value=""/>
    <SECN_KACD value=""/>
    <RGT_RSN_DTAIL_SORT_CD value=""/>
    <LIST_TPCD value=""/>
    <START_PAGE value="1"/>
    <END_PAGE value="15"/>
</reqParam>
```

### Response Sample (XML Extract)
```xml
<result>
    <RGT_STD_DT value="20260330"/>
    <TH1_PAY_TERM_BEGIN_DT value="20260423"/>
    <DELI_DT value=""/>
    <KN_DIV_PAY_DT value=""/>
    <SHOTN_ISIN value="098460"/>
    <KOR_SECN_NM value="고영테크놀러지"/>
    <LIST_TPNM value="코스닥시장"/>
    <RGT_RSN_DTAIL_SORT_NM value="현금배당"/>
    <SECN_DTAIL_KANM value="보통주"/>
    <CASH_ALOC_AMT value="140"/>
    <DIFF_ALOC_AMT value=""/>
    <CASH_ALOC_RATIO value="140"/>
    <STK_ALOC_RATIO value="0"/>
    <ESTM_STDPRC value="0"/>
    <PVAL value="100"/>
    <SETACC_MM value="12"/>
    <AG_ORG_TPNM value="한국예탁결제원"/>
</result>
```
