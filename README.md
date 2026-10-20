# How VLAE Works

**Variational Lossy Autoencoder — 디코더가 못 하는 것만 z에 담긴다.** Chen, Kingma, Salimans 외(ICLR 2017)의 「Variational Lossy Autoencoder」를 브라우저에서 직접 실험하며 배우는 인터랙티브 교육 자료입니다. 강한 자기회귀 디코더가 잠재 코드 z를 버리는 이유를 Bits-Back 코딩으로 설명하고, 그 원리를 뒤집어 **디코더의 수용 영역을 좁히면 지역 텍스처는 디코더가, 전역 구조만 z가 담게 된다**는 것을 장난감 VLAE를 실제로 학습시켜 확인합니다.

🔗 **[데모 바로가기](https://dev-jonghoonpark.github.io/how-vlae-works/)**

## 다루는 내용

1. **좋은 표현: 전역 구조와 지역 텍스처** · 12×12 장난감 데이터(모양 6 × 위치 4 = 4.58비트 + 마르코프 굵기 텍스처), 전역/지역을 따로 다시 뽑기
2. **VAE와 ELBO** · 식 (2)~(4). 1차원 가우시안에서 복원·KL·ELBO·log p(x)와 간극 KL(q‖p(z|x))을 닫힌 꼴로 계산, w = 0이면 q = 사전분포
3. **Bits-Back 코딩** · 식 (5)~(11). 6비트 메시지 하나의 코드 장부 — 두 단계 코드, 돌려받는 H(q), −ELBO, z 없이 보낸 길이
4. **강한 디코더는 왜 z를 버리는가** · 정보 선호. 독립 디코더 vs 자기회귀 디코더 VAE를 정확한 ELBO로 학습하면 자기회귀 쪽은 KL → 0, −ELBO = H(data) = 5.167비트
5. **VLAE: 디코더의 시야를 좁힌다** · 3.1절. 창(A×B) 크기만 바꾼 장난감 VLAE 7개 — z의 정보량 13.0 → 5.6비트, NLL 19.6 → 14.5비트, z 없는 같은 디코더와 비교. 브라우저에서 다시 학습 가능
6. **손실 압축** · 4.1절(19.2비트 vs 37.3비트). 압축 해제 결과와 전역 유지율(98.5% → 66.5%), 흑백 수용 영역(그림 3d)
7. **자기회귀 흐름 사전분포** · 식 (12)~(14). 같은 q를 ε 공간과 z 공간에서 보기, 평균만 쓰는 AF
8. **논문의 실험 결과** · 표 1~5, 부록 D 절제, CIFAR10 창 크기(그림 3·4), soft free bits
9. **그다음** · 비율–왜곡 평면(Alemi 외 2018), PixelVAE, VQ-VAE, δ-VAE, Lagging Inference Networks, 잠재 공간 생성 모델
10. **퀴즈** 7문항

## 참고

- Chen 외 (2017), *Variational Lossy Autoencoder*, ICLR 2017 — [arXiv:1611.02731](https://arxiv.org/abs/1611.02731)
- Kingma 외 (2016), *Improving Variational Inference with Inverse Autoregressive Flow* — [arXiv:1606.04934](https://arxiv.org/abs/1606.04934)
- Alemi 외 (2018), *Fixing a Broken ELBO* — [arXiv:1711.00464](https://arxiv.org/abs/1711.00464)

장난감 VLAE의 가중치는 페이지에 들어 있는 학습 코드로 미리 학습해 8비트로 줄여 `weights.json`에 따로 두었고, 첫 화면이 뜬 뒤 불러옵니다.

[how-ai-works](https://github.com/dev-jonghoonpark/how-ai-works) 시리즈의 일부입니다.
