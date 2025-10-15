# 🚗 DDui-DDui-Ride (뛰뛰라이드)

<div align="center">
  <img width="100%" src="./public/foreadme.gif" alt="DDui-DDui-Ride Demo"/>
  
  **실시간 경로 계산과 결제 기능을 갖춘 차량 호출 웹 애플리케이션**
  
  [🌐 Live Demo](https://ddui-ddui-ride.vercel.app/)
</div>

## 소개

Uber와 유사한 차량 호출 서비스를 구현한 웹 애플리케이션입니다. Google Maps API를 활용한 실시간 경로 계산 및 시각화, Stripe 결제 시스템을 지원합니다.

---

## 주요 기능

- 🗺️ **지도 및 경로**: Google Places API 기반 장소 검색, 실시간 경로 계산 및 시각화
- 🚘 **차량 선택**: 5가지 차량 타입 제공, 거리 기반 요금 계산
- 💳 **결제**: Stripe 통합 카드 결제 시스템
- 🔐 **인증**: Clerk 기반 회원가입 및 로그인

---

## 기술 스택

- **Framework**: Next.js 14, React 18, TypeScript
- **Styling**: Tailwind CSS, shadcn/ui
- **State Management**: Recoil
- **Maps**: Google Maps API, @react-google-maps/api
- **Payment**: Stripe
- **Authentication**: Clerk
- **Deployment**: Vercel

---

## 시작하기

### 사전 요구사항

- Node.js 18.0 이상
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

## 라이선스

This project is licensed under the MIT License.

---

## 참고

이 프로젝트는 [Build Full Stack NextJs 13 Uber Clone Web App](https://www.youtube.com/watch?v=pwsjvnADNGk&t=6594s) 강의를 참고하여 제작되었으며, 한국 환경에 맞게 수정 및 커스터마이징했습니다.
