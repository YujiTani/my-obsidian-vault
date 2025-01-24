---
tags:
  - note
  - JavaScript
---
> [!IMPORTANT]
> このテンプレート[[02_note]]の内容（見出しNote）はサンプルです。
> ご自分にとって使いやすいように編集してください。

## note

![[caroucel7.mp4]]

# 概要
## どんな機能か
- 無限ループできること
- 一定秒数ごとに自動でスライドすること
- 再生・停止だ操作できること
- next, prev操作ができること

## 大事だった部分
1. 要素が端までスライドした際に、transitionをnoneにしてX軸移動させる(それによってユーザーに移動してると気づかせないで移動させられる)
2. 要素の末端にクローン要素を追加する
3. イベントリスナーに`transitionend`を使うことでトランジションの移動終了時に、処理を実行させることができる


```
document.addEventListener('DOMContentLoaded', () => {
  const carouselConfig = {
    initialIndex: 1,
    slideWidthPercentage: 60,
    initialPositionPercentage: 100,
    autoplayInterval: 3000,
    transitionDuration: '1s',
  };

  const track = document.querySelector('.carousel-track');
  const slides = document.querySelectorAll('.carousel-slide');
  const prevButton = document.querySelector('.prev');
  const nextButton = document.querySelector('.next');
  const pauseButton = document.querySelector('.pause');

  // クローンを作成
  const firstSlideClone = slides[0].cloneNode(true);
  const secondSlideClone = slides[1].cloneNode(true);
  const lastSlideClone = slides[slides.length - 1].cloneNode(true);
  const secondLastSlideClone = slides[slides.length - 2].cloneNode(true);

  // クローンを挿入
  track.insertBefore(lastSlideClone, track.firstElementChild);
  track.insertBefore(secondLastSlideClone, track.firstElementChild);
  track.appendChild(firstSlideClone);
  track.appendChild(secondSlideClone);

  const slideCount = slides.length;

  let currentIndex = carouselConfig.initialIndex;
  let isPlaying = true;
  let intervalId;
  let isTransitioning = false;

  initSlidePosition();

  function initSlidePosition() {
    track.style.transform = `translateX(-${carouselConfig.initialPositionPercentage}%)`;
  }

  function updateSlidePosition(withTransition = true) {
    if (!withTransition) {
      track.style.transition = 'none';
    }

    track.style.transform = `translateX(-${carouselConfig.initialPositionPercentage + (currentIndex - 1) * carouselConfig.slideWidthPercentage}%)`;

    if (!withTransition) {
      track.offsetHeight;
      track.style.transition = `transform ${carouselConfig.transitionDuration} ease`;
    }
  }

  // スライドの移動が終了したときに実行
  function handleTransitionEnd() {
    if (isTransitioning) {
      isTransitioning = false;

      if (currentIndex >= slideCount + 1) {
        currentIndex = 1;
        updateSlidePosition(false);
      } else if (currentIndex <= 0) {
        currentIndex = slideCount;
        updateSlidePosition(false);
      }
    }
  }

  function moveToNextSlide() {
    if (isTransitioning) return;
    isTransitioning = true;
    currentIndex++;
    updateSlidePosition(true);
  }

  function moveToPrevSlide() {
    if (isTransitioning) return;
    isTransitioning = true;
    currentIndex--;

    if (currentIndex <= 0) {
      track.style.transform = `translateX(-40%)`;
      return;
    }
    updateSlidePosition(true);
  }

  function toggleAutoplay() {
    if (isPlaying) {
      clearInterval(intervalId);
      pauseButton.textContent = '▶';
    } else {
      startAutoplay();
      pauseButton.textContent = '⏸';
    }
    isPlaying = !isPlaying;
  }

  function startAutoplay() {
    intervalId = setInterval(moveToNextSlide, carouselConfig.autoplayInterval);
  }

  track.addEventListener('transitionend', handleTransitionEnd);

  nextButton.addEventListener('click', () => {
    moveToNextSlide();
    if (isPlaying) {
      clearInterval(intervalId);
      startAutoplay();
    }
  });

  prevButton.addEventListener('click', () => {
    moveToPrevSlide();
    if (isPlaying) {
      clearInterval(intervalId);
      startAutoplay();
    }
  });

  pauseButton.addEventListener('click', toggleAutoplay);

  startAutoplay();
});

```


