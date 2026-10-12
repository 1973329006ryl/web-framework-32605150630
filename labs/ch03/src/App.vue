<template>
  <div id="app">
    <div class="page-header">
      <h1>ch03-组件 | 第 3 章实验台</h1>
      <p class="subtitle">第03课下半场（3.1—3.7）：两种 API · 生命周期 · 注册 · 样式冲突 · 螺旋桨 / 发射 / 注入</p>
      <nav class="tab-nav">
        <a href="#exp-01" class="tab">01 两种API</a>
        <a href="#exp-02" class="tab">02 生命周期</a>
        <a href="#exp-03" class="tab">03 注册</a>
        <a href="#exp-04" class="tab">04 样式冲突</a>
        <a href="#exp-05" class="tab">05 props</a>
        <a href="#exp-06" class="tab">06 emit</a>
        <a href="#exp-07" class="tab">07 provide/inject</a>
      </nav>
    </div>

    <!-- 实验01 -->
    <section id="exp-01" class="doc-card">
      <h2>实验 01 | 选项式 API vs 组合式 API（3.1）</h2>
      <p class="desc">教材例 3-1 / 例 3-2 原文对照：同一个计数器，两种写法。</p>
      <div class="two-col">
        <CountOptions />
        <CountSetup />
      </div>
    </section>

    <!-- 实验02 -->
    <section id="exp-02" class="doc-card">
      <h2>实验 02｜生命周期（3.2）</h2>
      <p class="desc">挂载 → 点 +1（更新）→ 卸载（unmounted，Console 看清理）。子组件的 mount 先于父组件。</p>
      <LifecycleDemo />
      <p class="foot-note">↑ LifecycleDemo（父，"开关壳"）自己的 mount 也会在 Console 打印——顺序：LifecycleLab 先、Demo 后。</p>
    </section>

    <!-- 实验03 -->
    <section id="exp-03" class="doc-card">
      <h2>实验 03｜组件注册（3.3）</h2>
      <p class="desc">左：局部注册（App 的 components 选项）｜右：全局注册（main.js 的 app.component，App 里没有 import）</p>
      <div class="two-col">
        <LocalDemo />
        <GlobalDemo />
      </div>
    </section>

    <!-- 实验04 -->
    <section id="exp-04" class="doc-card">
      <h2>实验 04｜样式冲突与 scoped（3.4）</h2>
      <p class="desc">F12 检查下面的盒子：标签上带 data-v-xxxx 哈希属性——scoped 给选择器"加锁"。</p>
      <ScopedLab />
    </section>

    <!-- 实验05 -->
    <section id="exp-05" class="doc-card">
      <h2>实验 05｜props 父传子（3.5）</h2>
      <p class="desc">PriceBox 用对象方式声明 props（type/required/default）；点按钮故意传错类型，看 Console 警告。</p>
      <PropsLab />
    </section>

    <!-- 实验06 -->
    <section id="exp-06" class="doc-card">
      <h2>实验 06｜emit 子传父（3.6）</h2>
      <p class="desc">记忆模型：父 —props（只读）→ 子；父 ←@监听— emit（报信）— 子。</p>
      <EmitLab />
    </section>

    <!-- 实验07 -->
    <section id="exp-07" class="doc-card">
      <h2>实验 07｜provide / inject 跨级（3.7）</h2>
      <p class="desc">爷爷（本组件）provide 一辆车；中间层 MiddleChild 零传递；孙子 GrandChild 直接 inject。</p>
      <ProvideInjectLab />
    </section>
  </div>
</template>

<script>
import CountOptions from './experiments/01-apis/CountOptions.vue'
import CountSetup from './experiments/01-apis/CountSetup.vue'
import LifecycleDemo from './experiments/02-lifecycle/LifecycleDemo.vue'
import LocalDemo from './experiments/03-register/LocalDemo.vue'
import ScopedLab from './experiments/04-scoped/ScopedLab.vue'
import PropsLab from './experiments/05-props/PropsLab.vue'
import EmitLab from './experiments/06-emit/EmitLab.vue'
import ProvideInjectLab from './experiments/07-provide-inject/ProvideInjectLab.vue'

export default {
  name: 'App',
  components: {
    CountOptions,
    CountSetup,
    LifecycleDemo,
    LocalDemo,
    ScopedLab,
    PropsLab,
    EmitLab,
    ProvideInjectLab
  }
}
</script>

<style>
:root {
  --primary-green: #22c55e;
  --primary: #22c55e;
  --purple-line: #9333ea;
  --accent: #9333ea;
  --text-gray: #555;
  --muted: #666;
  --border: #e5e7eb;
  --border-light: #e5e7eb;
  --bg-page: #fcfcfd;
  --bg-card: #ffffff;
  --card: #ffffff;
  --radius: 10px;
  --shadow: 0 2px 8px rgb(17 24 39 / 5%);
  color-scheme: light;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background-color: var(--bg-page);
  font-family: system-ui, -apple-system, sans-serif;
  color: #333;
  font-size: 14px;
  line-height: 1.6;
}

#app {
  width: 100%;
  max-width: 980px;
  margin: 0 auto;
  padding: 28px 16px 40px;
  color: #333;
  font-family: system-ui, -apple-system, "Segoe UI", sans-serif;
  font-size: 14px;
  line-height: 1.6;
  text-align: left;
}

.page-header {
  text-align: center;
  margin-bottom: 26px;
}

.page-header h1 {
  font-size: 22px;
  line-height: 1.35;
  font-weight: 700;
  letter-spacing: 0;
  color: #111827;
  margin: 0 0 6px;
}

.subtitle {
  color: var(--text-gray);
  font-size: 14px;
  margin: 0 0 16px;
}

.tab-nav {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 8px;
}

.tab {
  padding: 5px 12px;
  border: 1px solid #86efac;
  border-radius: 999px;
  color: #15803d;
  background: #fff;
  text-decoration: none;
  font-size: 13px;
  line-height: 1.5;
  transition: background-color .15s ease, border-color .15s ease;
}

.tab:hover {
  background-color: #ecfdf3;
  border-color: var(--primary-green);
}

.doc-card {
  background: var(--bg-card);
  border: 1px solid var(--border-light);
  border-radius: 10px;
  padding: 20px;
  margin-bottom: 18px;
  box-shadow: var(--shadow);
}

#exp-02,
#exp-04,
#exp-05,
#exp-06,
#exp-07 {
  border-left: 4px solid var(--purple-line);
}

#app .lab {
  background: transparent;
  border: 0;
  border-radius: 0;
  box-shadow: none;
  padding: 0;
}

#app .lab > h2 {
  display: none;
}

.count-button {
  border: 0;
  border-radius: 6px;
  padding: 6px 14px;
  color: #fff;
  background: var(--primary-green);
  font: inherit;
  cursor: pointer;
}

.count-button:hover {
  background: #16a34a;
}

.count-button:focus-visible {
  outline: 2px solid #15803d;
  outline-offset: 2px;
}

#app button {
  border: 1px solid #16a34a;
  border-radius: 6px;
  padding: 6px 12px;
  color: #fff;
  background: var(--primary-green);
  font: inherit;
  line-height: 1.5;
  cursor: pointer;
  transition: background-color .15s ease, border-color .15s ease;
}

#app button:hover {
  border-color: #15803d;
  background: #16a34a;
}

#app button:focus-visible {
  outline: 2px solid #15803d;
  outline-offset: 2px;
}

.doc-card h2 {
  text-align: center;
  font-size: 17px;
  line-height: 1.45;
  font-weight: 650;
  margin: 0 0 8px;
  color: #222;
}

.desc {
  text-align: center;
  color: var(--text-gray);
  font-size: 14px;
  margin: 0 0 16px;
}

.two-col {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 14px;
}

#app .mini {
  border: 1px dashed var(--border);
  border-radius: 8px;
  padding: 12px 14px;
  background: #fff;
  text-align: center;
}

#app .mini h3 {
  margin: 0 0 8px;
  color: #222;
  font-size: 15px;
  line-height: 1.5;
}

#app .mini p {
  margin: 0 0 10px;
}

#app .inner {
  border-color: var(--accent);
  background: #fff;
}

#app .logs {
  background: #23272e;
  color: #c9e3d6;
  line-height: 1.8;
}

#app .box {
  border-color: var(--primary);
  background: #fff;
}

#app .deep-zone .box {
  border-color: #dc2626;
}

#app .middle {
  border-color: var(--accent);
  background: #fff;
}

#app .grand {
  border-color: var(--primary);
  background: #fff;
}

#app .muted,
.foot-note {
  color: #666;
}

#app .pair {
  grid-template-columns: repeat(2, minmax(0, 1fr));
}

.foot-note {
  font-size: 13px;
  margin-top: 10px;
}

@media (max-width: 700px) {
  #app {
    padding: 22px 14px 32px;
  }

  .doc-card {
    padding: 16px;
  }

  .two-col {
    grid-template-columns: 1fr;
  }

  #app .pair {
    grid-template-columns: 1fr;
  }
}
</style>
