<template>
  <div class="kato-wrapper">
    <div class="kato-mascot">
      <img src="/kato.png" alt="Kato 黑猫吉祥物" class="kato-img" />
      <div class="speech-bubble">
        <span>今天也要记得学习哦~</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.kato-wrapper {
  display: flex;
  justify-content: center;
}

.kato-mascot {
  position: relative;
  width: 130px;
  height: auto;
}

.kato-img {
  width: 100%;
  height: auto;
  object-fit: contain;
}

.speech-bubble {
  position: absolute;
  top: -8px;
  left: 100%;
  margin-left: 12px;
  background: var(--color-white);
  padding: 10px 18px;
  border-radius: 20px;
  box-shadow: var(--shadow-md);
  font-size: 14px;
  color: var(--color-gray-800);
  font-weight: 500;
  white-space: nowrap;
}

.speech-bubble::before {
  content: '';
  position: absolute;
  top: 50%;
  right: 100%;
  transform: translateY(-50%);
  border-top: 6px solid transparent;
  border-bottom: 6px solid transparent;
  border-right: 10px solid var(--color-white);
}
</style>
