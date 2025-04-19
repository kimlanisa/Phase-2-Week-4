# Phase-2-Week-4

# 📘 State Management dengan Redux

## 1. Apa itu Redux?
Redux adalah **library JavaScript** yang digunakan untuk mengelola *state global* dalam aplikasi, terutama yang menggunakan React. Redux membantu menjaga *state* agar tetap terorganisir, prediktif, dan mudah untuk di-*debug*.

---

## 2. Kenapa Menggunakan Redux?
- ✅ State terpusat (single source of truth)
- 🔁 Prediktif (karena state hanya bisa diubah lewat action → reducer)
- 🐛 Mudah di-debug (dengan DevTools)
- ♻️ Reusable dan scalable
- 🔍 Cocok untuk aplikasi besar dengan banyak komponen berbagi state

---

## 3. Konsep Utama Redux

| Konsep     | Penjelasan |
|------------|------------|
| **Store**  | Tempat penyimpanan semua state |
| **Action** | Objek yang mendeskripsikan perubahan state |
| **Reducer**| Fungsi yang menentukan bagaimana state berubah berdasarkan action |
| **Dispatch** | Metode untuk mengirim action ke reducer |
| **Selector** | Fungsi untuk mengambil state dari store |

---

## 4. Alur Kerja Redux (Flow)

```
View (React)
   ↓ (dispatch)
Action (Plain JS Object)
   ↓
Reducer (Pure Function)
   ↓
Store (State Updated)
   ↓
UI Re-render
```

---

## 5. Struktur File Redux (Contoh)

```
/redux
  ├── actions/
  │    └── counterActions.js
  ├── reducers/
  │    └── counterReducer.js
  └── store.js
```

---

## 6. Implementasi Dasar Redux

### a. Install Redux dan React-Redux

```bash
npm install redux react-redux
```

### b. Membuat Store

```js
// redux/store.js
import { createStore } from 'redux';
import counterReducer from './reducers/counterReducer';

const store = createStore(counterReducer);

export default store;
```

### c. Membuat Reducer

```js
// redux/reducers/counterReducer.js
const initialState = { count: 0 };

function counterReducer(state = initialState, action) {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

export default counterReducer;
```

### d. Membuat Action

```js
// redux/actions/counterActions.js
export const increment = () => ({ type: 'INCREMENT' });
export const decrement = () => ({ type: 'DECREMENT' });
```

### e. Hubungkan Store ke React

```js
// index.js
import React from 'react';
import ReactDOM from 'react-dom/client';
import { Provider } from 'react-redux';
import App from './App';
import store from './redux/store';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

---

## 7. Menggunakan Redux di Komponen

```js
// Counter.js
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement } from './redux/actions/counterActions';

function Counter() {
  const count = useSelector((state) => state.count);
  const dispatch = useDispatch();

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => dispatch(increment())}>Tambah</button>
      <button onClick={() => dispatch(decrement())}>Kurang</button>
    </div>
  );
}

export default Counter;
```

---

## 8. Redux DevTools
Tambahkan untuk debugging:

```js
const store = createStore(
  counterReducer,
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
);
```

---

## 9. Kapan Harus Menggunakan Redux?
Gunakan Redux jika:
- Banyak komponen perlu berbagi state
- Ada banyak jenis data/halaman berbeda
- Membutuhkan logging, debugging, dan devtools
- Context API sudah tidak cukup scalable
