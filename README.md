# Minimal Example – Leptos ServerFn + Actix State Behavior

This repository contains a **non-functional, minimal example** built to illustrate an issue I encountered when using server functions in [Leptos](https://leptos.dev) and Actix Web state.

It is based on the official Leptos starter template.

---

## ❗ Disclaimer

⚠️ This project is **not meant to be usefull**, it is a **minimal reproduction case** that demonstrate a compiler behavior I encountered. See below for context.

---

## 🧠 Context

While working on a Leptos + Actix project, I got this error when compiling the front side of the app : 

```bash
Front compiling WASM
    Compiling trivial-actix-server-state-in-server-fn v0.1.0 
error[E0412]: cannot find type `ServerState` in the crate root
  --> src/app.rs:13:27
   |
13 |     let data: Data<crate::ServerState> = extract().await?;
   |                           ^^^^^^^^^^^ not found in the crate root

For more information about this error, try `rustc --explain E0412`.
error: could not compile `trivial-actix-server-state-in-server-fn` (lib) due to 1 previous error
```

This minimal repo is a trivial version of my project in order to better understand the problem and potentially open an issue or ask for help.

The proble was that the compiler check the body of server functions even if it doesn't compile it for the WASM (i.e. the lib target). 

Therefore, because `ServerState` is declared in `main.rs` the compiler doesn't find it's declaration on the lib target. Moving `ServerState` declaration to the app.rs was the way to solve this problem.


---

## 🛠️ What It Shows

- A compilation failure using an Actix state inside a server function
- A clean minimal repro for debugging, asking for help, or reporting issues

---

## 🔍 Notes

- This is a **debugging artifact**, not a real application.
- If you’re looking for a working Leptos + Actix template, start from [the official starter](https://github.com/leptos-rs/leptos/tree/main/examples/leptos_actix).

---

## 📄 License

Unlicense
