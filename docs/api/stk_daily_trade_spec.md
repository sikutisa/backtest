# [API Spec] 유가증권 일별매매정보

## Overview
유가증권시장에 상장되어 있는 주권의 매매정보를 제공하는 서비스입니다. 본 API는 **2010년 01월 04일** 데이터부터 제공됩니다.

## Endpoint
`https://data-dbg.krx.co.kr/svc/apis/sto/stk_bydd_trd`

## Request (InBlock_1)
| 파라미터명 | 타입 | 설명 |
| :--- | :--- | :--- |
| basDd | string | 기준일자 (YYYYMMDD) |

## Response (OutBlock_1)
| 필드명 | 타입 | 설명 |
| :--- | :--- | :--- |
| BAS_DD | string | 기준일자 |
| ISU_CD | string | 종목코드 |
| ISU_NM | string | 종목명 |
| MKT_NM | string | 시장구분 |
| SECT_TP_NM | string | 소속부 |
| TDD_CLSPRC | string | 종가 |
| CMPPREVDD_PRC | string | 대비 |
| FLUC_RT | string | 등락률 |
| TDD_OPNPRC | string | 시가 |
| TDD_HGPRC | string | 고가 |
| TDD_LWPRC | string | 저가 |
| ACC_TRDVOL | string | 거래량 |
| ACC_TRDVAL | string | 거래대금 |
| MKTCAP | string | 시가총액 |
| LIST_SHRS | string | 상장주식수 |

## Samples

### Request Sample
```json
{
  "basDd": "20240102"
}
```

### Response Sample
```json
{
  "OutBlock_1": [
    {
      "BAS_DD": "20240102",
      "ISU_CD": "005930",
      "ISU_NM": "삼성전자",
      "MKT_NM": "KOSPI",
      "SECT_TP_NM": "주권",
      "TDD_CLSPRC": "79600",
      "CMPPREVDD_PRC": "1100",
      "FLUC_RT": "1.40",
      "TDD_OPNPRC": "78200",
      "TDD_HGPRC": "79800",
      "TDD_LWPRC": "78200",
      "ACC_TRDVOL": "22877482",
      "ACC_TRDVAL": "1815858639500",
      "MKTCAP": "475194685780000",
      "LIST_SHRS": "5969782550"
    }
  ]
}
```
