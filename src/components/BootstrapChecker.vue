<template>
  <div class="checker-wrapper bg-body min-vh-100">
    <!-- Theme Toggle (Fixed Top Right) -->
    <div class="theme-toggle-fixed">
      <div class="form-check form-switch bg-body border rounded-pill px-4 py-3 shadow-sm d-flex align-items-center gap-2 shadow-lg">
        <label class="form-check-label small fw-bold" for="themeSwitch">
          <span v-if="theme === 'light'">☀️</span>
          <span v-else>🌙</span>
        </label>
        <input 
          class="form-check-input m-0 ms-3" 
          type="checkbox" 
          role="switch" 
          id="themeSwitch"
          :checked="theme === 'dark'"
          @change="toggleTheme"
        >
      </div>
    </div>

    <!-- Header -->
    <header class="bg-primary text-white py-5 shadow-sm">
      <div class="container">
        <h1 class="fw-bold mb-1">Bootstrap Customize Demo</h1>
        <p class="opacity-75 mb-0">用來驗證 Bootstrap 變數覆寫是否成功套用</p>
      </div>
    </header>

    <!-- Sticky Navigation -->
    <nav class="checker-nav sticky-top bg-body border-bottom shadow-sm">
      <div class="container py-5">
        <ul class="nav nav-pills flex-wrap gap-4">
          <!-- Core Style Items -->
          <li v-for="item in coreItems" :key="item.id" class="nav-item">
            <a 
              class="nav-link py-1 px-3 small fw-bold" 
              :class="{ active: activeSection === item.id }" 
              :href="'#' + item.id"
              @click="handleNavClick(item.id)"
            >
              {{ item.label }}
            </a>
          </li>

          <!-- Components Group Toggle -->
          <li class="nav-item">
            <button 
              class="nav-link py-1 px-3 small fw-bold d-flex align-items-center gap-1 border"
              :class="{ active: isComponentActive }"
              @click="isComponentsExpanded = !isComponentsExpanded"
            >
              <span>元件項目</span>
              <small>{{ isComponentsExpanded ? '▲' : '▼' }}</small>
            </button>
          </li>

          <!-- Expanded Component Items -->
          <template v-if="isComponentsExpanded">
            <li v-for="item in componentItems" :key="item.id" class="nav-item">
              <a 
                class="nav-link py-1 px-3 small btn-component border" 
                :class="{ active: activeSection === item.id }" 
                :href="'#' + item.id"
                @click="handleNavClick(item.id)"
              >
                {{ item.label }}
              </a>
            </li>
          </template>
        </ul>
      </div>
    </nav>

    <div class="container py-7">
      <!-- ───────────────────────────────── Typography ─── -->
      <section id="typography" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Typography / 標題</div>
        <div class="card-body p-7 position-relative">
          <!-- Hidden elements for White/Black color extraction -->
          <div class="d-none">
            <div id="swatch-white" class="text-white"></div>
            <div id="swatch-black" class="text-black"></div>
          </div>
          <h1 class="mb-4">H1 — 主要標題 Heading 1</h1>
          <h2 class="mb-4">H2 — 次要標題 Heading 2</h2>
          <h3 class="mb-3">H3 — 三級標題 Heading 3</h3>
          <h4 class="mb-3">H4 — 四級標題 Heading 4</h4>
          <hr class="my-6" />
          <p class="lead mb-5">Lead — 引言段落文字，用於頁面開頭的摘要描述</p>
          <p class="mb-5">
            Body — 一般正文段落，Lorem ipsum dolor sit amet, consectetur
            adipiscing elit. Sed do eiusmod tempor incididunt ut labore.
          </p>
          <div class="d-flex gap-4">
            <span class="text-muted small">text-muted — 次要說明文字</span>
            <span class="small border-start ps-4">small — 小字，用於版權聲明等</span>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Colors ─── -->
      <section id="colors" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Theme Colors / 主題色彩</div>
        <div class="card-body p-7">
          <div class="row g-7">
            <div v-for="color in themeColors" :key="color.name" class="col-12 border-bottom pb-6">
              <div class="fw-bold text-capitalize mb-5 d-flex align-items-center gap-3">
                <span class="fs-5">{{ color.label }}</span>
                <span class="badge bg-dark border small fw-normal px-3 py-2">{{ colorRegistry[`theme-${color.name}`]?.hex }}</span>
              </div>
              
              <div class="row g-6">
                <!-- Solid Swatch -->
                <div class="col-md-4">
                  <div :id="`swatch-${color.name}`" :class="`bg-${color.name}`" class="rounded-3 p-5 text-center border shadow-sm mb-3">
                    <span :class="color.name === 'light' ? 'text-dark' : 'text-white'" class="small font-monospace fw-bold">.bg-{{ color.name }}</span>
                  </div>
                  <div class="small font-monospace opacity-75">
                    <code>--bs-{{ color.name }}</code>
                  </div>
                </div>

                <!-- Subtle Swatch -->
                <div class="col-md-4">
                  <div :id="`swatch-${color.name}-subtle`" :class="`bg-${color.name}-subtle`" class="rounded-3 p-5 text-center border shadow-sm mb-3">
                    <span :class="`text-${color.name}-emphasis`" class="small font-monospace fw-bold">.bg-{{ color.name }}-subtle</span>
                  </div>
                  <div class="small font-monospace opacity-75 d-flex justify-content-between">
                    <code>--bg-subtle</code>
                    <span class="badge bg-body-secondary text-muted fw-normal">{{ colorRegistry[`subtle-${color.name}`]?.hex }}</span>
                  </div>
                </div>

                <!-- Components -->
                <div class="col-md-4 d-flex flex-column justify-content-center gap-3">
                  <div class="d-flex gap-3">
                    <button class="btn btn-sm flex-grow-1" :class="`btn-${color.name}`">Button</button>
                    <button class="btn btn-sm flex-grow-1" :class="`btn-outline-${color.name}`">Outline</button>
                  </div>
                  <div class="d-flex align-items-center gap-3">
                    <span class="badge flex-grow-1 py-2" :class="`bg-${color.name}`">Badge</span>
                    <span class="badge rounded-pill flex-grow-1 py-2" :class="`bg-${color.name}`">Pill</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Base Color Scales ─── -->
      <section id="scales" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Base Color Scales / 基礎色階</div>
        <div class="card-body p-7">
          <div v-for="colorName in allBaseColors" :key="colorName" class="mb-4">
            <h6 class="text-capitalize mb-4 border-bottom pb-2 fs-5 fw-bold">{{ colorName }}</h6>
            <div class="row g-3">
              <div v-for="level in colorLevels" :key="level" class="col">
                <div 
                  :id="`base-${colorName}-${level}`"
                  class="rounded-2 mb-2 shadow-sm border"
                  :style="{ backgroundColor: `var(--bs-${colorName}-${level})`, height: '40px' }"
                ></div>
                <div class="text-center" style="font-size: 0.7rem;">
                  <div class="fw-bold mb-1">{{ level }}</div>
                  <div class="text-muted">{{ colorRegistry[`base-${colorName}-${level}`]?.hex }}</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Spacers ─── -->
      <section id="spacers" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Spacers / 間距系統 ($spacers)</div>
        <div class="card-body p-5 p-0">
          <div v-for="s in spacers" :key="s" class="row g-0 align-items-center border-bottom py-4 px-5">
            <div class="col-2 fw-bold"><code>$spacer-{{ s }}</code></div>
            <div class="col-2"><span class="font-monospace px-3 py-2">{{ spacerRegistry[s] }}</span></div>
            <div class="col-8">
              <div class="d-flex align-items-center bg-body-secondary border p-2 rounded-3 overflow-hidden" style="max-width: 100%;">
                <div 
                  :id="`spacer-box-${s}`"
                  class="bg-primary rounded-2"
                  :class="`me-${s}`"
                  style="width: 32px; height: 32px; flex-shrink: 0;"
                ></div>
                <div class="bg-primary rounded-2 opacity-25 shadow-sm" style="width: 32px; height: 32px; flex-shrink: 0;"></div>
                <div class="ms-4 small text-secondary">這兩個方塊之間的間距為 {{ spacerRegistry[s] }}</div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Border Radius ─── -->
      <section id="radius" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Border Radius / 圓角系統</div>
        <div class="card-body p-7">
          <div class="row g-7 d-flex">
            <div v-for="r in radii" :key="r.class" class="text-center w-auto">
              <div 
                :id="`radius-sample-${r.class}`"
                class="bg-primary bg-opacity-25 border border-primary border-2 mx-auto mb-3" 
                :class="r.class"
                style="width: 100px; height: 100px;"
              ></div>
              <code class="d-block fw-bold mb-1">{{ r.var }}</code>
              <div class="badge bg-dark px-3 py-2 fw-normal">{{ radiusShadowRegistry[`radius-${r.class}`] }}</div>
              <code class="d-block small mt-1">.{{ r.class }}</code>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Box Shadow ─── -->
      <section id="shadows" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Box Shadows / 陰影系統</div>
        <div class="card-body p-7">
          <div class="row g-7 py-3">
            <div v-for="s in shadows" :key="s.class" class="col-md-3">
              <div :id="`shadow-sample-${s.class}`" class="p-5 text-center rounded-3 bg-body border" :class="s.class">
                <span class="fw-bold">.{{ s.class }}</span>
              </div>
              <div class="mt-4 text-center">
                <code class="fw-bold d-block mb-1">{{ s.var }}</code>
                <div class="text-muted small text-truncate border rounded bg-body-secondary p-2 font-monospace" style="font-size: 0.65rem;">
                  {{ radiusShadowRegistry[`shadow-${s.class}`] }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Body BG ─── -->
      <section id="bg" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Body Background / 背景色</div>
        <div class="card-body p-7">
          <div class="row g-4">
            <div class="col-md-4" v-for="bgClass in ['bg-body', 'bg-body-secondary', 'bg-body-tertiary', 'bg-white', 'bg-light']" :key="bgClass">
              <div :class="bgClass" class="p-5 border rounded-3 text-center fw-bold font-monospace shadow-sm">.{{ bgClass }}</div>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── UI Components Header ─── -->
      <div class="py-5 border-top mt-10 mb-5">
        <h2 class="fw-bold mb-2">UI 元件驗證區域</h2>
        <p class="text-muted lead">確認 Bootstrap 元件在覆寫變數後的樣式表現</p>
      </div>

      <!-- ───────────────────────────────── Buttons ─── -->
      <section id="buttons" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Buttons / 按鈕</div>
        <div class="card-body p-7">
          <div class="mb-7">
            <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">按鈕顏色、外框與連結 (Solid, Outline & Link)</div>
            <div class="d-flex flex-wrap gap-4">
              <button v-for="color in themeColors" :key="color.name" :class="`btn btn-${color.name}`" class="px-4">
                {{ color.label }}
              </button>
            </div>
            <div class="d-flex flex-wrap gap-4 mt-4">
              <button v-for="color in themeColors" :key="color.name" :class="`btn btn-outline-${color.name}`" class="px-4">
                {{ color.label }}
              </button>
            </div>
            <div class="d-flex flex-wrap gap-4 mt-4">
              <button v-for="color in themeColors" :key="color.name" :class="['btn btn-link', 'link-' + color.name]" class="px-4">
                {{ color.label }}
              </button>
            </div>
          </div>
          <div class="mb-7">
            <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">按鈕尺寸 (Sizes)</div>
            <div class="d-flex flex-wrap align-items-center gap-5">
              <button class="btn btn-primary btn-lg px-5">Large Button</button>
              <button class="btn btn-primary px-4">Default Button</button>
              <button class="btn btn-primary btn-sm px-3">Small Button</button>
            </div>
          </div>
          <div>
            <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">按鈕狀態矩陣 (States Matrix)</div>
            <div v-for="type in buttonTypes" :key="type.id" class="mb-6">
              <h6 class="mb-4 text-primary fw-bold">{{ type.label }} Variant</h6>
              <div class="row g-4">
                <div v-for="state in buttonStates" :key="state.id" class="col-xl col-md-4 col-sm-6">
                  <div class="p-4 border rounded-3 bg-body-tertiary h-100">
                    <div class="d-flex justify-content-center mb-4" style="min-height: 45px;">
                      <button :id="`btn-state-${type.id}-${state.id}`" class="btn px-4" :class="[type.class, state.class]">
                        <span v-if="state.hasSpinner" class="spinner-border spinner-border-sm me-2"></span>
                        {{ state.label }}
                      </button>
                    </div>
                    
                    <div class="small">
                      <!-- Background Color -->
                      <div class="mb-3">
                        <div class="fw-bold mb-1 d-flex justify-content-between">
                          <span>Background</span>
                          <div class="text-end">
                            <code :class="buttonRegistry[`${type.id}-${state.id}`]?.bg === 'Transparent' ? 'text-muted' : 'text-primary'">
                              {{ buttonRegistry[`${type.id}-${state.id}`]?.bg }}
                            </code>
                            <div v-if="buttonRegistry[`${type.id}-${state.id}`]?.bgAlpha !== '1' && buttonRegistry[`${type.id}-${state.id}`]?.bg !== 'Transparent'" class="small text-muted" style="font-size: 0.65rem;">
                              Alpha: {{ buttonRegistry[`${type.id}-${state.id}`]?.bgAlpha }}
                            </div>
                          </div>
                        </div>
                        <div class="mb-2">
                          <small class="text-muted">Match: </small>
                          <span class="badge bg-secondary-subtle text-secondary-emphasis border small fw-normal">
                            {{ buttonRegistry[`${type.id}-${state.id}`]?.bgMatch }}
                          </span>
                        </div>
                        <div class="text-muted opacity-75 font-monospace" style="font-size: 0.7rem;">
                          CSS: {{ state.cssVars[0] }}<br>
                          SCSS: {{ state.scssVars[0] }}
                        </div>
                      </div>

                      <!-- Text Color -->
                      <div class="mb-3 pt-3 border-top">
                        <div class="fw-bold mb-1 d-flex justify-content-between">
                          <span>Text Color</span>
                          <div class="text-end">
                            <code class="text-primary">{{ buttonRegistry[`${type.id}-${state.id}`]?.text }}</code>
                            <div v-if="buttonRegistry[`${type.id}-${state.id}`]?.textAlpha !== '1'" class="small text-muted" style="font-size: 0.65rem;">
                              Alpha: {{ buttonRegistry[`${type.id}-${state.id}`]?.textAlpha }}
                            </div>
                          </div>
                        </div>
                        <div class="mb-2">
                          <small class="text-muted">Match: </small>
                          <span class="badge bg-secondary-subtle text-secondary-emphasis border small fw-normal">
                            {{ buttonRegistry[`${type.id}-${state.id}`]?.textMatch }}
                          </span>
                        </div>
                        <div class="text-muted opacity-75 font-monospace" style="font-size: 0.7rem;">
                          CSS: {{ state.cssVars[2] }}<br>
                          SCSS: {{ state.scssVars[2] }}
                        </div>
                      </div>
                      
                      <!-- Border Color -->
                      <div class="mb-3 pt-3 border-top">
                        <div class="fw-bold mb-1 d-flex justify-content-between">
                          <span>Border</span>
                          <code class="text-primary">{{ buttonRegistry[`${type.id}-${state.id}`]?.border }}</code>
                        </div>
                        <div class="mb-2">
                          <small class="text-muted">Match: </small>
                          <span class="badge bg-secondary-subtle text-secondary-emphasis border small fw-normal">
                            {{ buttonRegistry[`${type.id}-${state.id}`]?.borderMatch }}
                          </span>
                        </div>
                        <div class="text-muted opacity-75 font-monospace" style="font-size: 0.7rem;">
                          CSS: {{ state.cssVars[1] }}<br>
                          SCSS: {{ state.scssVars[1] }}
                        </div>
                      </div>

                      <div class="pt-2 border-top">
                        <div class="fw-bold mb-1 d-flex justify-content-between">
                          <span>Opacity</span>
                          <code class="text-info">{{ buttonRegistry[`${type.id}-${state.id}`]?.opacity }}</code>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Badges & Alerts ─── -->
      <section id="badges" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Badges / 徽章標籤</div>
        <div class="card-body p-7">
          <div class="d-flex flex-wrap gap-4 mb-6">
            <span v-for="color in themeColors" :key="color.name" :class="`badge bg-${color.name}`" class="px-3 py-2 fs-6">
              {{ color.label }}
            </span>
          </div>
          <div class="d-flex flex-wrap gap-4">
            <span v-for="color in themeColors" :key="color.name" :class="`badge rounded-pill bg-${color.name}`" class="px-4 py-2 fs-6">
              Pill {{ color.label }}
            </span>
          </div>
        </div>
      </section>

      <section id="alerts" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Alerts / 提示訊息</div>
        <div class="card-body p-7">
          <div class="row g-5">
            <div v-for="color in themeColors" :key="color.name" class="col-md-6">
              <div :class="`alert alert-${color.name}`" class="py-4 px-5 mb-0 shadow-sm border-2">
                <strong class="text-capitalize">{{ color.label }} Alert</strong><br>
                這是 <code>.alert-{{ color.name }}</code> 的樣式呈現。
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Forms ─── -->
      <section id="forms" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Forms / 表單元件</div>
        <div class="card-body p-7">
          <!-- Input Sizes -->
          <div class="mb-7">
            <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">輸入框尺寸 (Input Sizes)</div>
            <div class="row g-5 align-items-end">
              <div class="col-md-4">
                <label class="form-label small fw-bold">Large (.form-control-lg)</label>
                <input type="text" class="form-control form-control-lg" placeholder="Large input" />
              </div>
              <div class="col-md-4">
                <label class="form-label small fw-bold">Default</label>
                <input type="text" class="form-control" placeholder="Default input" />
              </div>
              <div class="col-md-4">
                <label class="form-label small fw-bold">Small (.form-control-sm)</label>
                <input type="text" class="form-control form-control-sm" placeholder="Small input" />
              </div>
            </div>
          </div>

          <!-- Input States -->
          <div class="mb-7">
            <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">輸入框狀態 (Input States)</div>
            <div class="row g-5">
              <div class="col-md-4">
                <label class="form-label small fw-bold">Disabled (禁用)</label>
                <input type="text" class="form-control" value="這個欄位無法輸入" disabled />
              </div>
              <div class="col-md-4">
                <label class="form-label small fw-bold">Readonly (唯讀)</label>
                <input type="text" class="form-control" value="僅供檢視，無法修改" readonly />
              </div>
              <div class="col-md-4">
                <label class="form-label small fw-bold">Plaintext (純文字)</label>
                <input type="text" readonly class="form-control-plaintext border-bottom" value="email@example.com" />
              </div>
              <div class="col-md-6">
                <label class="form-label small fw-bold text-success">Valid State (驗證成功)</label>
                <input type="text" class="form-control is-valid" value="正確的內容" />
                <div class="valid-feedback">看起來不錯！這個樣式反映了 $form-feedback-valid-color</div>
              </div>
              <div class="col-md-6">
                <label class="form-label small fw-bold text-danger">Invalid State (驗證失敗)</label>
                <input type="text" class="form-control is-invalid" value="錯誤的內容" />
                <div class="invalid-feedback">請輸入有效資訊。這個樣式反映了 $form-feedback-invalid-color</div>
              </div>
            </div>
          </div>

          <!-- Select & Other Controls -->
          <div class="mb-7">
            <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">下拉選單與特殊元件 (Select & Others)</div>
            <div class="row g-5">
              <div class="col-md-4">
                <label class="form-label small fw-bold">Select LG</label>
                <select class="form-select form-select-lg">
                  <option selected>開啟選單</option>
                  <option value="1">選項一</option>
                </select>
              </div>
              <div class="col-md-4">
                <label class="form-label small fw-bold">Select Default</label>
                <select class="form-select">
                  <option selected>預設尺寸</option>
                  <option value="1">選項一</option>
                </select>
              </div>
              <div class="col-md-4">
                <label class="form-label small fw-bold">Select SM</label>
                <select class="form-select form-select-sm">
                  <option selected>小尺寸</option>
                  <option value="1">選項一</option>
                </select>
              </div>
              <div class="col-md-6">
                <label class="form-label small fw-bold">Range (範圍滑桿)</label>
                <input type="range" class="form-range" id="customRange1">
              </div>
              <div class="col-md-6">
                <label class="form-label small fw-bold">Floating Label (浮動標籤)</label>
                <div class="form-floating">
                  <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
                  <label for="floatingInput">Email address</label>
                </div>
              </div>
            </div>
          </div>

          <!-- Checkboxes & Radios -->
          <div>
            <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">勾選與單選 (Checks & Radios)</div>
            <div class="row g-5">
              <div class="col-md-4">
                <div class="form-check mb-3">
                  <input class="form-check-input border-2" type="checkbox" id="checkActive" checked>
                  <label class="form-check-label" for="checkActive">作用中的 Checkbox</label>
                </div>
                <div class="form-check">
                  <input class="form-check-input border-2" type="checkbox" id="checkDisabled" disabled>
                  <label class="form-check-label" for="checkDisabled">禁用的 Checkbox</label>
                </div>
              </div>
              <div class="col-md-4">
                <div class="form-check mb-3">
                  <input class="form-check-input border-2" type="radio" name="radioTest" id="radio1" checked>
                  <label class="form-check-label" for="radio1">選中的 Radio</label>
                </div>
                <div class="form-check">
                  <input class="form-check-input border-2" type="radio" name="radioTest" id="radio2">
                  <label class="form-check-label" for="radio2">未選的 Radio</label>
                </div>
              </div>
              <div class="col-md-4">
                <div class="form-check form-switch mb-3">
                  <input class="form-check-input border-2" type="checkbox" id="switch1" checked>
                  <label class="form-check-label" for="switch1">開啟的 Switch</label>
                </div>
                <div class="form-check form-switch">
                  <input class="form-check-input border-2" type="checkbox" id="switch2">
                  <label class="form-check-label" for="switch2">關閉的 Switch</label>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Cards ─── -->
      <section id="cards" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Cards / 卡片元件</div>
        <div class="card-body p-7">
          <div class="row g-7">
            <div class="col-md-4">
              <div class="card h-100 shadow-sm border-2">
                <div class="card-header fw-bold">標配卡片</div>
                <div class="card-body">
                  <h5 class="card-title">標題文字</h5>
                  <p class="card-text text-muted">這是標準卡片的內容描述區域。</p>
                  <a href="#" class="btn btn-primary btn-sm">按鈕動作</a>
                </div>
              </div>
            </div>
            <div class="col-md-4">
              <div class="card h-100 bg-primary text-white border-0 shadow">
                <div class="card-body p-5 text-center">
                  <h5 class="fw-bold mb-3">主題色卡片</h5>
                  <p class="mb-4">套用了 .bg-primary 的背景樣式。</p>
                  <button class="btn btn-light btn-sm px-4">了解更多</button>
                </div>
              </div>
            </div>
            <div class="col-md-4">
              <div class="card h-100 border-success border-2">
                <div class="card-body d-flex flex-column justify-content-between">
                  <h5 class="text-success fw-bold">成功狀態卡片</h5>
                  <p class="small">邊框與文字顏色受 $success 變數控制。</p>
                  <div class="badge bg-success py-2">已驗證</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Tables ─── -->
      <section id="tables" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Tables / 表格元件</div>
        <div class="card-body p-7">
          <div class="table-responsive">
            <table class="table table-hover table-bordered border-2 align-middle">
              <thead class="table-dark text-uppercase small font-monospace">
                <tr>
                  <th class="p-3">狀態標籤</th>
                  <th class="p-3">項目名稱</th>
                  <th class="p-3 text-center">數據數值</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="color in themeColors.slice(0, 5)" :key="color.name" :class="`table-${color.name}`">
                  <td class="p-3"><span :class="`badge bg-${color.name}`">Active</span></td>
                  <td class="p-3 fw-bold">項目 {{ color.label }}</td>
                  <td class="p-3 text-center font-monospace">{{ color.width }}%</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── List Group ─── -->
      <section id="list-group" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">List Group / 清單群組</div>
        <div class="card-body p-7">
          <div class="row g-7">
            <div class="col-md-6">
              <ul class="list-group shadow-sm border-2">
                <li class="list-group-item active py-3 d-flex justify-content-between align-items-center">
                  作用中的項目
                  <span class="badge bg-white text-primary rounded-pill">14</span>
                </li>
                <li v-for="n in 3" :key="n" class="list-group-item py-3">一般清單項目 {{ n }}</li>
                <li class="list-group-item disabled py-3 bg-body-secondary">禁用項目樣式</li>
              </ul>
            </div>
            <div class="col-md-6">
              <div class="list-group border-0 gap-2">
                <a v-for="color in themeColors.slice(0, 4)" :key="color.name" href="#" 
                   :class="`list-group-item list-group-item-${color.name} list-group-item-action border rounded-3 p-3 fw-bold`">
                  標籤連結：{{ color.label }}
                </a>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Navs & Pagination ─── -->
      <section id="navs" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Navs & Pagination / 導覽與分頁</div>
        <div class="card-body p-7">
          <div class="row g-7">
            <!-- Tabs & Pills -->
            <div class="col-md-6">
              <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">Tabs & Pills / 分頁與膠囊</div>
              <ul class="nav nav-tabs mb-4">
                <li class="nav-item"><a class="nav-link active" href="#">Active</a></li>
                <li class="nav-item"><a class="nav-link" href="#">Link</a></li>
                <li class="nav-item"><a class="nav-link disabled" href="#">Disabled</a></li>
              </ul>
              <ul class="nav nav-pills">
                <li class="nav-item"><a class="nav-link active" href="#">Active</a></li>
                <li class="nav-item"><a class="nav-link border mx-1" href="#">Link</a></li>
                <li class="nav-item"><a class="nav-link disabled" href="#">Disabled</a></li>
              </ul>
            </div>
            
            <!-- Pagination -->
            <div class="col-md-6">
              <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">Pagination / 分頁按鈕</div>
              <nav aria-label="Page navigation example">
                <ul class="pagination mb-4">
                  <li class="page-item disabled"><a class="page-link" href="#">Previous</a></li>
                  <li class="page-item"><a class="page-link" href="#">1</a></li>
                  <li class="page-item active"><a class="page-link" href="#">2</a></li>
                  <li class="page-item"><a class="page-link" href="#">3</a></li>
                  <li class="page-item"><a class="page-link" href="#">Next</a></li>
                </ul>
                <ul class="pagination pagination-sm">
                  <li class="page-item active"><a class="page-link" href="#">1</a></li>
                  <li class="page-item"><a class="page-link" href="#">2</a></li>
                </ul>
              </nav>
            </div>

            <!-- Breadcrumbs -->
            <div class="col-12 mt-2">
              <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">Breadcrumbs / 麵包屑</div>
              <nav aria-label="breadcrumb">
                <ol class="breadcrumb bg-body-secondary p-3 rounded-3 shadow-sm">
                  <li class="breadcrumb-item"><a href="#">首頁</a></li>
                  <li class="breadcrumb-item"><a href="#">元件庫</a></li>
                  <li class="breadcrumb-item active" aria-current="page">當前頁面</li>
                </ol>
              </nav>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Dropdowns & Input Groups ─── -->
      <section id="dropdowns" class="card mb-8 shadow-sm scroll-mt">
        <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Dropdowns & Input Groups / 下拉與群組</div>
        <div class="card-body p-7">
          <div class="row g-7">
            <!-- Dropdowns -->
            <div class="col-md-5">
              <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">Dropdown Menu / 下拉選單樣式</div>
              <div class="dropdown-menu position-static d-block shadow-sm border-2">
                <h6 class="dropdown-header">選單標題</h6>
                <a class="dropdown-item active" href="#">作用中的項目</a>
                <a class="dropdown-item" href="#">一般項目樣式</a>
                <hr class="dropdown-divider">
                <a class="dropdown-item disabled" href="#">禁用的項目</a>
              </div>
            </div>

            <!-- Input Groups -->
            <div class="col-md-7">
              <div class="small fw-bold text-uppercase text-muted mb-4 border-bottom pb-2">Input Groups / 輸入框群組</div>
              <div class="input-group mb-4">
                <span class="input-group-text bg-primary text-white border-primary">@</span>
                <input type="text" class="form-control" placeholder="Username">
              </div>
              <div class="input-group mb-4">
                <input type="text" class="form-control" placeholder="Recipient's username">
                <button class="btn btn-outline-primary" type="button">按鈕</button>
              </div>
              <div class="input-group">
                <span class="input-group-text">$</span>
                <input type="text" class="form-control" aria-label="Amount (to the nearest dollar)">
                <span class="input-group-text">.00</span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ───────────────────────────────── Progress & Spinners ─── -->
      <div class="row g-8">
        <div class="col-md-7">
          <section id="progress" class="card h-100 shadow-sm scroll-mt">
            <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Progress / 進度條</div>
            <div class="card-body p-7">
              <div v-for="color in themeColors.slice(0, 4)" :key="color.name" class="mb-5">
                <div class="d-flex justify-content-between small fw-bold mb-2">
                  <span class="text-uppercase">{{ color.label }}</span>
                  <span class="font-monospace">{{ color.width }}%</span>
                </div>
                <div class="progress shadow-sm" style="height: 1.25rem;">
                  <div :class="`progress-bar bg-${color.name} progress-bar-striped progress-bar-animated`" 
                       :style="`width: ${color.width}%`" role="progressbar"></div>
                </div>
              </div>
            </div>
          </section>
        </div>
        <div class="col-md-5">
          <section id="spinners" class="card h-100 shadow-sm scroll-mt">
            <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Spinners / 載入動畫</div>
            <div class="card-body p-7 d-flex flex-wrap justify-content-center gap-5">
              <div v-for="color in themeColors" :key="color.name" class="text-center">
                <div :class="`spinner-border text-${color.name}`" role="status" style="width: 2.5rem; height: 2.5rem; border-width: 0.3em;"></div>
                <div :class="`spinner-grow text-${color.name} mt-3 d-block mx-auto`" role="status" style="width: 1.5rem; height: 1.5rem;"></div>
              </div>
            </div>
          </section>
        </div>
      </div>

      <!-- ───────────────────────────────── Accordion & Toast ─── -->
      <div class="row g-8 mt-4">
        <div class="col-md-6">
          <section id="accordion" class="card h-100 shadow-sm scroll-mt">
            <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Accordion / 手風琴</div>
            <div class="card-body p-7">
              <div class="accordion shadow-sm" id="checkerAccordion">
                <div class="accordion-item border-2">
                  <h2 class="accordion-header">
                    <button class="accordion-button fw-bold py-4" type="button" data-bs-toggle="collapse" data-bs-target="#acc1">
                      展開狀態檢查
                    </button>
                  </h2>
                  <div id="acc1" class="accordion-collapse collapse show" data-bs-parent="#checkerAccordion">
                    <div class="accordion-body p-4 text-muted">
                      測試 Accordion 展開後的背景色與文字間距。
                    </div>
                  </div>
                </div>
                <div class="accordion-item border-2 border-top-0">
                  <h2 class="accordion-header">
                    <button class="accordion-button collapsed fw-bold py-4" type="button" data-bs-toggle="collapse" data-bs-target="#acc2">
                      收合樣式檢查
                    </button>
                  </h2>
                  <div id="acc2" class="accordion-collapse collapse" data-bs-parent="#checkerAccordion">
                    <div class="accordion-body p-4">
                      這是收合內容測試。
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </section>
        </div>
        <div class="col-md-6">
          <section id="toasts" class="card h-100 shadow-sm scroll-mt">
            <div class="card-header bg-body-tertiary fw-bold small text-uppercase py-3 px-5">Toasts / 通知提示</div>
            <div class="card-body p-7 bg-body-secondary bg-opacity-10 d-flex justify-content-center align-items-center">
              <div class="toast show border-0 shadow-lg" role="alert" style="min-width: 320px;">
                <div class="toast-header bg-primary text-white py-3">
                  <strong class="me-auto">系統通知</strong>
                  <small>剛剛</small>
                  <button type="button" class="btn-close btn-close-white" data-bs-dismiss="toast"></button>
                </div>
                <div class="toast-body p-4 fw-bold">
                  這是 Toast 的內容。檢查其陰影 ($toast-box-shadow) 與圓角。
                </div>
              </div>
            </div>
          </section>
        </div>
      </div>

      <div class="text-center mt-10 opacity-50 small">
        &copy; Bootstrap Customize Demo - 完整變數驗證工具
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, nextTick } from "vue";

const themeColors = [
  { name: "primary", label: "Primary", width: 80 },
  { name: "secondary", label: "Secondary", width: 65 },
  { name: "success", label: "Success", width: 70 },
  { name: "danger", label: "Danger", width: 45 },
  { name: "warning", label: "Warning", width: 55 },
  { name: "info", label: "Info", width: 60 },
  { name: "light", label: "Light", width: 30 },
  { name: "dark", label: "Dark", width: 95 },
];

const allBaseColors = ["blue", "indigo", "purple", "pink", "red", "orange", "yellow", "green", "teal", "cyan", "gray"];
const colorLevels = [100, 200, 300, 400, 500, 600, 700, 800, 900];
const spacers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
const radii = [
  { class: "rounded-0", var: "$border-radius-0" },
  { class: "rounded-1", var: "$border-radius-sm" },
  { class: "rounded-2", var: "$border-radius" },
  { class: "rounded-3", var: "$border-radius-lg" },
  { class: "rounded-4", var: "$border-radius-xl" },
  { class: "rounded-5", var: "$border-radius-xxl" },
  { class: "rounded-circle", var: "$border-radius-circle" },
  { class: "rounded-pill", var: "$border-radius-pill" },
];
const shadows = [
  { class: "shadow-none", var: "none" },
  { class: "shadow-sm", var: "$box-shadow-sm" },
  { class: "shadow", var: "$box-shadow" },
  { class: "shadow-lg", var: "$box-shadow-lg" },
];

const buttonTypes = [
  { id: 'solid', label: 'Solid', class: 'btn-primary' },
  { id: 'outline', label: 'Outline', class: 'btn-outline-primary' },
  { id: 'link', label: 'Link', class: 'btn-link' }
];

const buttonStates = [
  { id: 'normal', label: 'Normal', class: '', cssVars: ['--bs-btn-bg', '--bs-btn-border-color', '--bs-btn-color'], scssVars: ['$primary', '$primary', '#ffffff'] },
  { id: 'hover', label: 'Hover', class: 'hover-state', cssVars: ['--bs-btn-hover-bg', '--bs-btn-hover-border-color', '--bs-btn-hover-color'], scssVars: ['$btn-hover-bg', '$btn-hover-border-color', '$btn-hover-color'] },
  { id: 'active', label: 'Active', class: 'active border-3', cssVars: ['--bs-btn-active-bg', '--bs-btn-active-border-color', '--bs-btn-active-color'], scssVars: ['$btn-active-bg', '$btn-active-border-color', '$btn-active-color'] },
  { id: 'disabled', label: 'Disabled', class: 'disabled', cssVars: ['--bs-btn-disabled-bg', '--bs-btn-disabled-border-color', '--bs-btn-disabled-color'], scssVars: ['$btn-disabled-bg', '$btn-disabled-border-color', '$btn-disabled-color'] },
  { id: 'loading', label: 'Loading', class: '', hasSpinner: true, cssVars: ['--bs-btn-bg', '--bs-btn-border-color', '--bs-btn-color'], scssVars: ['$primary', '$primary', '#ffffff'] }
];

const coreItems = [
  { id: 'typography', label: '字體排版' },
  { id: 'colors', label: '主題色彩' },
  { id: 'scales', label: '基礎色階' },
  { id: 'spacers', label: '間距系統' },
  { id: 'radius', label: '圓角系統' },
  { id: 'shadows', label: '陰影系統' },
  { id: 'bg', label: '背景色彩' },
];

const componentItems = [
  { id: 'buttons', label: '按鈕元件' },
  { id: 'badges', label: '徽章標籤' },
  { id: 'alerts', label: '提示訊息' },
  { id: 'forms', label: '表單元件' },
  { id: 'cards', label: '卡片元件' },
  { id: 'tables', label: '表格元件' },
  { id: 'list-group', label: '清單群組' },
  { id: 'navs', label: '導覽與分頁' },
  { id: 'dropdowns', label: '下拉與群組' },
  { id: 'accordion', label: '手風琴' },
  { id: 'progress', label: '進度條' },
  { id: 'spinners', label: '載入動畫' },
  { id: 'toasts', label: '通知提示' },
];

const navItems = [...coreItems, ...componentItems];
const activeSection = ref('typography');
const isComponentsExpanded = ref(true); // Default expanded for better discoverability

const theme = ref(document.documentElement.getAttribute('data-bs-theme') || 'light');

const toggleTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light';
  document.documentElement.setAttribute('data-bs-theme', theme.value);
  // Also update registry to reflect new computed colors if needed
  nextTick(() => {
    updateRegistry();
  });
};

const isComponentActive = computed(() => {
  return componentItems.some(item => item.id === activeSection.value);
});

const handleNavClick = (id) => {
  activeSection.value = id;
};

const setupScrollspy = () => {
  const options = {
    root: null,
    rootMargin: '-100px 0px -70% 0px',
    threshold: 0
  };

  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        activeSection.value = entry.target.id;
        if (componentItems.some(item => item.id === entry.target.id)) {
          isComponentsExpanded.value = true;
        }
      }
    });
  }, options);

  navItems.forEach((item) => {
    const el = document.getElementById(item.id);
    if (el) observer.observe(el);
  });
};

const colorRegistry = ref({});
const spacerRegistry = ref({});
const radiusShadowRegistry = ref({});
const buttonRegistry = ref({});

const rgbToHex = (r, g, b) => {
  return "#" + [r, g, b].map(x => parseInt(x).toString(16).padStart(2, '0')).join("").toUpperCase();
};

const parseColor = (colorStr) => {
  if (!colorStr || colorStr === "rgba(0, 0, 0, 0)" || colorStr === "transparent") {
    return { hex: "Transparent", alpha: "0" };
  }
  const rgba = colorStr.match(/^rgba?\((\d+),\s*(\d+),\s*(\d+)(?:,\s*([\d.]+))?\)/);
  return rgba ? { 
    hex: rgbToHex(rgba[1], rgba[2], rgba[3]),
    alpha: rgba[4] || "1"
  } : { hex: "N/A", alpha: "1" };
};

const extractColor = (id, prop = null) => {
  const el = document.getElementById(id);
  if (!el) return { hex: "N/A", alpha: "1" };
  const style = window.getComputedStyle(el);
  
  if (prop) {
    return parseColor(style[prop]);
  }
  
  // Legacy fallback behavior for swatches
  const bg = style.backgroundColor;
  const colorStr = bg && bg !== "rgba(0, 0, 0, 0)" && bg !== "transparent" ? bg : style.color;
  return parseColor(colorStr);
};

const extractStyle = (id, prop) => {
  const el = document.getElementById(id);
  return el ? window.getComputedStyle(el)[prop] : "N/A";
};

const updateRegistry = () => {
  const registry = {};
  const sRegistry = {};
  const rsRegistry = {};
  const bRegistry = {};
  
  // Extract White and Black first
  registry['white'] = extractColor('swatch-white');
  registry['black'] = extractColor('swatch-black');

  themeColors.forEach(color => {
    registry[`theme-${color.name}`] = extractColor(`swatch-${color.name}`);
    registry[`subtle-${color.name}`] = extractColor(`swatch-${color.name}-subtle`);
  });

  allBaseColors.forEach(color => {
    colorLevels.forEach(level => registry[`base-${color}-${level}`] = extractColor(`base-${color}-${level}`));
  });

  spacers.forEach(s => sRegistry[s] = extractStyle(`spacer-box-${s}`, 'marginRight'));
  radii.forEach(r => rsRegistry[`radius-${r.class}`] = extractStyle(`radius-sample-${r.class}`, 'borderRadius'));
  shadows.forEach(s => rsRegistry[`shadow-${s.class}`] = extractStyle(`shadow-sample-${s.class}`, 'boxShadow'));

  const findMatch = (hex) => {
    if (!hex || hex === 'N/A' || hex === 'Transparent') return 'none';
    
    // Check fundamental colors first
    if (hex === registry['white']?.hex) return 'white';
    if (hex === registry['black']?.hex) return 'black';

    let match = 'none';
    for (const [key, value] of Object.entries(registry)) {
      if (value.hex === hex) {
        // Prefer theme names or base scale names, stripping prefixes
        const cleanName = key.replace('theme-', '').replace('base-', '').replace('subtle-', '(subtle) ');
        
        // If we found a base scale or theme name, use it
        if (!key.includes('subtle-')) {
          return cleanName;
        }
        match = cleanName; // Fallback to subtle if no solid match found yet
      }
    }
    return match;
  };

  buttonTypes.forEach(type => {
    buttonStates.forEach(state => {
      const elementId = `btn-state-${type.id}-${state.id}`;
      const bgData = extractColor(elementId, 'backgroundColor');
      const textData = extractColor(elementId, 'color');
      
      let borderHex = extractStyle(elementId, 'borderColor');
      // Convert border color to hex if it's RGB
      if (borderHex.startsWith('rgb')) {
        const rgba = borderHex.match(/^rgba?\((\d+),\s*(\d+),\s*(\d+)/);
        if (rgba) borderHex = rgbToHex(rgba[1], rgba[2], rgba[3]);
      }

      bRegistry[`${type.id}-${state.id}`] = {
        bg: bgData.hex,
        bgAlpha: bgData.alpha,
        text: textData.hex,
        textAlpha: textData.alpha,
        border: borderHex,
        bgMatch: findMatch(bgData.hex),
        textMatch: findMatch(textData.hex),
        borderMatch: findMatch(borderHex),
        opacity: extractStyle(elementId, 'opacity')
      };
    });
  });

  colorRegistry.value = registry;
  spacerRegistry.value = sRegistry;
  radiusShadowRegistry.value = rsRegistry;
  buttonRegistry.value = bRegistry;
};

onMounted(() => {
  nextTick(() => {
    updateRegistry();
    setupScrollspy();
  });
});
</script>

<style scoped>
.scroll-mt {
  scroll-margin-top: 180px; /* Offset for multiline sticky nav pills */
}

.theme-toggle-fixed {
  position: fixed;
  top: 1rem;
  right: 1rem;
  z-index: 2000; /* Above everything */
}

/* Simulate hover states for the checker */
:deep(.btn.hover-state) {
  background-color: var(--bs-btn-hover-bg) !important;
  border-color: var(--bs-btn-hover-border-color) !important;
  color: var(--bs-btn-hover-color) !important;
}

/* For link buttons, hover often only changes color and decoration */
:deep(.btn-link.hover-state) {
  background-color: transparent !important;
  border-color: transparent !important;
  color: var(--bs-btn-hover-color) !important;
  text-decoration: underline !important;
}

/* For outline buttons, hover fills the background */
:deep(.btn-outline-primary.hover-state) {
  background-color: var(--bs-btn-hover-bg) !important;
  color: var(--bs-btn-hover-color) !important;
}
</style>
