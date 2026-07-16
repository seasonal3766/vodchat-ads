# vodchat-ads — 광고 관리 저장소

VOD 챗로그 확장의 사이드바 광고를 이 저장소 하나로 관리합니다.
**여기서 커밋하면 재배포 없이 모든 사용자에게 반영됩니다** (확장은 1시간 캐시로 갱신).

## 관리 방법 (전부 GitHub 웹에서 가능)

### 광고 추가/교체
1. `banners/` 폴더에 이미지 업로드 (Add file → Upload files)
   - 규격: **500×220 px** (표시 크기 250×110의 2배, 선명하게 나옴)
   - PNG/JPG, 500KB 이하 권장
2. `ad.json` 열어서 연필(✏️) 클릭 → 편집:
```json
{
  "enabled": true,
  "ads": [
    {
      "img": "https://raw.githubusercontent.com/seasonal3766/vodchat-ads/main/banners/파일명.png",
      "link": "https://이동할주소",
      "alt": "설명"
    }
  ]
}
```
3. Commit changes. 끝. (사용자들은 최대 1시간 안에 새 광고를 보게 됨)

### 여러 광고 로테이션
`ads` 배열에 여러 개 넣으면 확장이 열릴 때마다 **랜덤으로 1개** 표시됩니다.

### 광고 전체 끄기
`"enabled": false` 로 바꾸고 커밋. 모든 사용자의 슬롯이 숨겨집니다.

## 규칙 (확장 쪽 검증 로직)
- `img` 는 반드시 `https://` 로 시작해야 함 (아니면 그 항목 무시)
- `link` 는 http/https 허용
- JSON이 깨지거나 저장소 접근 불가 시: 마지막 캐시 사용, 그것도 없으면 슬롯 숨김 (확장이 죽지 않음)

## 저장소 설정
- 이 저장소는 **Public** 이어야 합니다 (raw.githubusercontent.com 으로 서빙되려면)
- 확장 코드의 `AD_REMOTE_URL` 상수가 이 저장소의 ad.json raw 주소를 가리켜야 합니다:
  `https://raw.githubusercontent.com/<계정>/vodchat-ads/main/ad.json`
