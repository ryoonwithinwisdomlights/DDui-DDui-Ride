# 🚗 [DDui-DDui-Ride (뛰뛰라이드)](https://ddui-ddui-ride.vercel.app/)

<div align="center">
  <img width="100%" src="./public/foreadme.gif" alt="DDui-DDui-Ride Demo"/>
  
  **실시간 경로 계산과 결제 기능을 갖춘 풀스택 차량 호출 서비스**
  
  [🌐 Live Demo](https://ddui-ddui-ride.vercel.app/) | [📹 프로젝트 영상](https://ddui-ddui-ride.vercel.app/)
</div>

---

## 📌 프로젝트 소개

**DDui-DDui-Ride**는 Uber와 유사한 차량 호출 서비스를 구현한 풀스택 웹 애플리케이션입니다. Google Maps API를 활용하여 실시간 경로 계산 및 시각화를 제공하며, Stripe를 통한 안전한 결제 처리를 지원합니다.

### 🎯 프로젝트 목표

- **Google Maps API 심층 학습**: Mapping library의 다양한 기능(Places API, Directions API, Custom Markers 등)을 실전에서 활용
- **한국 환경 최적화**: 해외 튜토리얼 기반 프로젝트를 한국 환경에 맞게 커스터마이징
- **풀스택 개발 경험**: 프론트엔드부터 결제 시스템까지 전체 플로우 구현

---

## ✨ 주요 기능

### 🗺️ 지도 및 경로 기능
- **실시간 장소 검색**: Google Places Autocomplete API를 활용한 출발지/도착지 검색
- **경로 시각화**: DirectionsRenderer를 통한 최적 경로 표시
- **커스텀 마커**: 출발지와 도착지를 구분하는 맞춤형 마커 및 레이블
- **동적 지도 이동**: 장소 선택 시 자동으로 해당 위치로 지도 중심 이동

### 🚘 차량 선택 시스템
- **다양한 차량 옵션**: Uber X, Comfort, XL, Pet, Black 등 5가지 차량 타입
- **실시간 요금 계산**: 거리 기반 동적 요금 산정
- **차량별 상세 정보**: 좌석 수, 특징, 가격 정보 제공

### 💳 결제 시스템
- **Stripe 통합**: 안전한 카드 결제 처리
- **결제 확인 페이지**: 결제 완료 후 예약 확인 화면

### 🔐 사용자 인증
- **Clerk 인증 시스템**: 안전한 회원가입 및 로그인
- **보호된 라우트**: 인증된 사용자만 서비스 이용 가능

---

## 🛠️ 기술 스택

### Frontend
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **UI Library**: React 18
- **Styling**: Tailwind CSS
- **UI Components**: shadcn/ui, Radix UI
- **State Management**: Recoil

### Backend & Services
- **API Routes**: Next.js API Routes
- **Maps**: Google Maps JavaScript API, @react-google-maps/api
- **Places**: Google Places API, react-google-places-autocomplete
- **Payment**: Stripe
- **Authentication**: Clerk

### Development Tools
- **Package Manager**: npm
- **Linting**: ESLint
- **Deployment**: Vercel

---

## 📁 프로젝트 구조

```
uber-eats-clone/
├── app/
│   ├── api/
│   │   └── create-intent/          # Stripe 결제 인텐트 생성 API
│   ├── components/
│   │   ├── Header.tsx              # 전역 헤더 컴포넌트
│   │   └── Home/
│   │       ├── SearchSection.tsx   # 출발지/도착지 검색 섹션
│   │       ├── GoogleMapSection.tsx # 지도 및 경로 표시
│   │       ├── CarListOptions.tsx  # 차량 선택 옵션
│   │       ├── CarListItem.tsx     # 개별 차량 아이템
│   │       ├── CheckoutForm.tsx    # 결제 폼
│   │       └── InputItem.tsx       # 검색 입력 컴포넌트
│   ├── payment/                    # 결제 페이지
│   ├── payment-confirm/            # 결제 확인 페이지
│   ├── sign-in/                    # 로그인 페이지
│   └── sign-up/                    # 회원가입 페이지
├── components/ui/                  # shadcn/ui 컴포넌트
├── context/                        # React Context
│   ├── SourceContext.ts
│   └── DestinationContext.ts
├── lib/
│   ├── states.ts                   # Recoil 상태 정의
│   └── utils.ts                    # 유틸리티 함수
├── utils/
│   └── CarListData.ts              # 차량 데이터
└── middleware.ts                   # Clerk 인증 미들웨어
```

---

## 🚀 시작하기

### 사전 요구사항

- Node.js 18.0 이상
- npm 또는 yarn
- Google Maps API Key
- Stripe API Key
- Clerk API Key

### 설치 및 실행

1. **레포지토리 클론**
```bash
git clone https://github.com/yourusername/uber-eats-clone.git
cd uber-eats-clone
```

2. **의존성 설치**
```bash
npm install
```

3. **환경 변수 설정**

`.env.local` 파일을 생성하고 다음 환경 변수를 추가합니다:

```env
# Google Maps
NEXT_PUBLIC_GOOGLE_API_KEY=your_google_maps_api_key
NEXT_PUBLIC_GOOGLE_MAP_API=your_google_map_id

# Stripe
NEXT_PUBLIC_STRIPE_PUBLISHER_KEY=your_stripe_publishable_key
STRIPE_SECRET_KEY=your_stripe_secret_key

# Clerk
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key
```

4. **개발 서버 실행**
```bash
npm run dev
```

5. **브라우저에서 확인**
```
http://localhost:3000
```

---

## 💡 핵심 구현 내용

### 1. Google Maps API 통합

**GoogleMapSection 컴포넌트**에서 복잡한 지도 기능을 구현했습니다:

```typescript
// 출발지/도착지 상태 변경 시 자동으로 지도 중심 이동
useEffect(() => {
  if (!isEmptyObj(source) && map) {
    map.panTo({ lat: source.lat, lng: source.lng });
    setCenter({ lat: source.lat, lng: source.lng });
  }
}, [source]);

// DirectionsRenderer를 통한 경로 표시
<DirectionsRenderer
  directions={directionRoutePoints}
  options={{
    polylineOptions: {
      strokeColor: "#393938",
      strokeWeight: 10,
    },
    suppressMarkers: true,
  }}
/>
```

### 2. 상태 관리 (Recoil)

전역 상태를 Recoil atom으로 관리하여 컴포넌트 간 데이터 공유:

- `sourceState`: 출발지 정보
- `destinationState`: 도착지 정보
- `directionRoutePoints`: 경로 정보
- `centerState`: 지도 중심 좌표

### 3. Stripe 결제 통합

API Route를 통한 안전한 결제 인텐트 생성:

```typescript
// app/api/create-intent/route.ts
const paymentIntent = await stripe.paymentIntents.create({
  amount: amount * 100, // 센트 단위로 변환
  currency: 'krw',
});
```

---

## 🔧 트러블슈팅 및 해결 과제

### 1. 한국 환경에서의 Google Maps API 제약

**문제**: Google Maps의 일부 기능(Transit Directions 등)이 한국에서 제한적으로 지원됨

**해결**: 
- Places API와 Directions API를 활용하여 기본 경로 계산 기능 구현
- 커스텀 마커와 오버레이를 사용하여 사용자 경험 개선

### 2. 비동기 지도 로딩 처리

**문제**: Google Maps API 로딩 전에 컴포넌트가 렌더링되어 에러 발생

**해결**:
- `LoadScript` 컴포넌트로 API 로딩 관리
- 조건부 렌더링으로 데이터 존재 여부 확인 후 UI 표시

```typescript
{!isEmptyObj(source) && !isEmptyObj(destination) && (
  <DirectionsRenderer directions={directionRoutePoints} />
)}
```

### 3. 타입 안정성 확보

**문제**: Google Maps API의 복잡한 타입 처리

**해결**:
- TypeScript를 활용한 타입 안전성 확보
- `@react-google-maps/api`의 타입 정의 활용

---

## 📚 배운 점 & 성장 경험

### 기술적 성장
- **Google Maps API 심층 이해**: Places, Directions, Marker, Overlay 등 다양한 API의 실전 활용 경험
- **상태 관리 전략**: Recoil을 활용한 효율적인 전역 상태 관리 패턴 학습
- **결제 시스템 구현**: Stripe를 통한 안전한 결제 플로우 구현 경험
- **인증 시스템**: Clerk를 활용한 모던 인증 시스템 통합

### 문제 해결 능력
- 해외 튜토리얼을 한국 환경에 맞게 커스터마이징하는 과정에서 발생한 다양한 이슈 해결
- Google Maps API의 지역별 제약사항을 파악하고 대안 마련
- TypeScript 환경에서의 외부 라이브러리 타입 처리 경험

### 프로젝트 관리
- 3일이라는 짧은 기간 내에 MVP 완성을 위한 우선순위 설정
- 기능 단위 개발 및 점진적 개선 방식 적용

---

## 🎨 주요 화면

### 메인 화면
- 출발지/도착지 검색
- 실시간 지도 업데이트
- 차량 선택 옵션

### 결제 화면
- Stripe 카드 입력 폼
- 예상 요금 표시

### 결제 완료
- 예약 확인 정보
- 차량 및 경로 요약

---

## 🔮 향후 개선 계획

- [ ] 실시간 차량 위치 추적 기능
- [ ] 운전자-승객 실시간 채팅
- [ ] 예약 내역 관리 페이지
- [ ] 다국어 지원 (i18n)
- [ ] PWA 구현으로 모바일 앱 경험 제공
- [ ] 즐겨찾기 장소 저장 기능
- [ ] 카카오맵 API 통합 (한국 환경 최적화)

---

## 📄 라이선스

This project is open source and available under the [MIT License](LICENSE).

---

## 🙏 참고 자료

이 프로젝트는 [Build Full Stack NextJs 13 Uber Clone Web App](https://www.youtube.com/watch?v=pwsjvnADNGk&t=6594s) 강의를 참고하여 제작되었으며, 한국 환경에 맞게 커스터마이징 및 기능을 추가했습니다.

---

## 👤 Contact

**개발 기간**: 2024년 (3일)

프로젝트에 대한 문의사항이나 피드백은 언제든 환영합니다!

---

<div align="center">
  <strong>Made with ❤️ by Ryoon</strong>
  
  ⭐ 이 프로젝트가 도움이 되었다면 Star를 눌러주세요!
</div>
