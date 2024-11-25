As a developer, I’ve always loved diving into new technologies and building cool things from scratch. But when it came to creating my personal site, I ended up overcomplicating things a little. Here’s the story of how I built it, what tools I used, and how I might have made it harder than it needed to be. 🤔💻

## The Tools: A Developer's Playground 🛠️🌍

Building a website is often as much about picking the right tools as it is about writing the code. For my site, I chose to work with **Rust** (blazingly fast! ⚡), **Yew** (think of it as React for Rust), and a few other gems to make the process smoother. 

### **Rust**: The Blazing Fast Core 🚀

Rust is the heart of this site. If you’ve ever worked with it, you’ll know that Rust is known for its speed and safety. Writing the back-end logic of my website in Rust felt like a natural choice, given its performance and control. The fact that I’m compiling down to WebAssembly (Wasm) only makes things faster and more efficient. ⚡

In hindsight, I could have probably made life easier by leveraging more established front-end frameworks like React, which I already extensively knew, from the get-go. But hey, where’s the fun in that? 😎

### **Yew**: React for Rust ⚛️🔧

Yew is a Rust framework for building front-end web apps. If you’ve ever used React, Yew will feel somewhat familiar. It allows you to build reactive UIs with Rust, which compiles to WebAssembly, hence **blazingly fast**. 💨 However, I didn’t have to go all in with Rust for every part of the website. A simpler approach might have been to use Rust just for the core logic and perhaps use other tools for more standard HTML-based content. But again, that wouldn’t have been as fun. 🤪

### **Trunk**: The Unsung Hero 🦸‍♂️

Now, here’s where things get interesting: **Trunk**. Trunk is a Wasm bundler that makes it ridiculously easy to compile Rust code into Wasm, serve assets, and even handle Tailwind CSS during development. Honestly, this tool is a **godsend**. 🙌 It manages everything for me — from building my code to hot-reloading during development. It's the real MVP of this project. 🏆

### **Tailwind CSS**: Speedy Styling 🎨

When it comes to styling, I am literal garbage, hence I wanted something that would allow me to build beautiful layouts quickly without fighting with CSS, so I could get back to the logic. Enter **Tailwind CSS**. It’s a utility-first CSS framework that lets you create custom designs without ever writing a single line of custom CSS. 🧑‍🎨 With Tailwind, I could focus on building the layout and styling the site quickly by just adding classes. 🔥

### **GitHub Pages & GitHub Actions**: Automating Deployment 🤖

Now, let’s talk **deployment**. I wanted my site to be as automated as possible, and since I’m already using GitHub, I figured, why not use **GitHub Pages** and **GitHub Actions** to handle deployment? 🛠️💡

Every time I push changes to my repository [pandecode/d3bug64](https://github.com/pandecode/d3bug64), GitHub Actions kicks in. The action runs the build process, compiles the Rust code, and pushes everything to my [pandecode/pandecode.github.io](https://github.com/pandecode/pandecode.github.io) repository. It’s a nice, streamlined process, but I’ll admit it adds some extra complexity to the project. 🔄

---

## The Directory Layout: Where Things Live 🗂️

To better understand how everything fits together, here’s a quick breakdown of my project structure:

```
├── Cargo.lock
├── Cargo.toml
├── README.md
├── Trunk.toml
├── assets
│   ├── {{ icons }}
│   ├── site.webmanifest
│   └── svgs
│       └── web.svg
├── dist
│   └── {{Build Outputs by trunk}}
├── index.css
├── index.html
├── rust-toolchain.toml
├── shell.nix
├── src
│   ├── components
│   │   ├── about.rs
│   │   ├── articles.rs
│   │   ├── home.rs
│   │   ├── mod.rs
│   │   ├── nav_bar.rs
│   │   ├── not_found.rs
│   │   └── projects.rs
│   ├── data.rs
│   ├── main.rs
│   ├── router.rs
│   ├── theme.rs
│   └── utils
│       ├── error.rs
│       ├── gh.rs
│       ├── github_projects_obj.rs
│       └── mod.rs
└── tailwind.config.js
```

- **Cargo.toml**: This is the manifest file for my Rust project. It defines dependencies like Yew and other libraries.
- **Trunk.toml**: Configures Trunk and specifies how to bundle the assets.
- **assets/**: Holds my site’s assets, like icons and the web manifest. Pretty standard for a web app. 🖼️
- **dist/**: Contains the build outputs from Trunk. This is where all the magic gets compiled. ✨
- **src/**: The source folder where all my Rust code lives, including the main logic for the website and components. ⚙️
- **tailwind.config.js**: Configures Tailwind CSS to suit my needs. 🎨

---

## Problems 🛠️

- The final build is about 300KB. I think I can get that number lower, but for now, loading the Wasm into the browser takes some time. However, compared to some React projects, mine's not too bad. 🤷‍♂️
- **Limitations of Web APIs with Wasm**: Old browsers don’t always support WebAssembly, so compatibility can be an issue. 🧑‍💻❌

---

## Conclusion: Overcomplicated, But Totally Worth It 🏁

Looking back, I realize that I overcomplicated the entire process. I could have gone with a simpler tech stack and been just fine. But as a developer, sometimes the joy comes from pushing boundaries, experimenting, and seeing how things fit together. It’s all part of the fun! 🎉

Feel free to explore the code:
[pandecode/d3bug64](https://github.com/pandecode/d3bug64)
