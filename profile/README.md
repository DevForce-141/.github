# DevForce 141 — Guidelines & Standards

# 🙋‍♀️ Introduction

DevForce 141 is a special task force of developers. At least, this is what we like to think of it. We are all friends joining up together to make great stuff, with a hope that the stuff will help us make even greater stuff. 🙂

---

## 🛠️ Our Tech Stack

We love Laravel and its ecosystem — specifically the **TALL Stack** (Tailwind CSS, AlpineJS, Livewire, Laravel).

### Languages

- PHP
- JavaScript
- C# *(only when PHP & JS can't be used)*
- Java *(only when PHP & JS can't be used)*

### Markup / Non-Programming Languages

> We don't want `definitions` wars, hence we're putting them here.

- HTML
- CSS
- SQL
- XML
- JSON

### Frameworks & Core Libraries (TALL Stack)

- **Laravel** — Backend Framework
- **Tailwind CSS** — Styling
- **Livewire** — Reactive UI
- **AlpineJS** — Lightweight JS Interactivity
- **Flux UI** — UI Components

### Additional Libraries

- **ReactJS / VueJS** — When SPA behaviour is needed
- **jQuery** — Legacy or minimal-JS projects only
- **Bootstrap** — Legacy projects only; prefer Tailwind

### CMS / Builds
- WordPress
- Shopify (Despised and avoided, we only maintain existing projects)

### Databases
- MySQL
- PostgreSQL
- MongoDB

### Clouds
- AWS
- Azure
- DigitalOcean

---

# 🌈 Guidelines for Requirements Providers / Clients

- If you're sharing something early-stage, say so explicitly and acknowledge its shortfalls. This avoids confusion and saves everyone's time.
- Be as explicit as you can. The more explicit you are, the higher the chance your message is received as intended.
- Don't assume others will magically figure things out. Give context and forward knowledge to your best ability.
  > **Example:** If providing a database dump, mention the DBMS name and version. Don't make others guess.

---

# 🌈 Development Guidelines

We like to understand the systems we build. We pay careful attention to semantics and naming, which keeps us free of confusion and maintains a clean codebase.

---

## 🧠 Understanding the Project

- Identify all entities in any project early on.
- Name entities semantically — closer to what they reflect. The more specific, the better.
  > **💡 Naming Example**
  >
  > In a crypto project where users initiate mining, prefer `MiningSession` over `Session`.
  > `Session` is a generic, overloaded term in computing — it often refers to something built into your language or framework entirely. The more specific name leaves zero room for confusion.
- Identify ambiguous requirements and missing bits early. There are always many.
- When in doubt, bring it up and clear it out. It will bite and hurt down the road otherwise.

---

## 💬 Communication

Communication is often the deciding factor between a good and bad outcome.

- Re-read and review whatever you write. Remove typos and verify your message conveys what you intend.
- Limit each sentence or clause to one topic. Don't jam multiple things into one.
- Use line breaks effectively to reduce clutter and make text easy on the eyes.
- Use punctuation extensively: comma `,`, semicolon `;`, full stop `.`, double quotes `""`.
- Wrap anything verbatim in double quotes — for example, when referring to a button label in a UI: click `"Save Changes"`.

---

## 🤖 AI-Assisted Development

We embrace AI tooling as a force multiplier, but with discipline. The goal is to ship quality code faster — not to blindly accept AI output.

### Mindset

> **⚠️ Golden Rule:** You are always responsible for the code you commit, regardless of how it was generated. Never commit AI-generated code you don't understand. If you can't explain it, you don't own it.

- AI is a **pair programmer**, not a replacement for understanding.
- AI is especially good at: boilerplate, test generation, refactoring suggestions, documentation, and exploring unfamiliar APIs. Lean on it for these.
- AI is unreliable for: business logic nuances, project-specific conventions, and security-sensitive code. Always review these areas carefully.

### Recommended Tools

- **[GitHub Copilot](https://github.com/features/copilot) / [Cursor](https://cursor.sh/)** — In-editor completions and chat
- **[Claude](https://claude.ai) / [ChatGPT](https://chatgpt.com)** — Architecture discussions, code review, debugging
- **[Laravel Idea](https://plugins.jetbrains.com/plugin/13441-laravel-idea)** — Laravel-specific intelligence in PhpStorm

### AI Workflow Guidelines

**Always provide context when prompting.**
AI output quality is proportional to context quality. Share the relevant model, your action class pattern, and point to these guidelines when asking for non-trivial tasks.

> **💡 Prompt Template Example**
> ```
> I'm working in a Laravel project that follows the Action Pattern using the
> Laravel Actions package. Actions are namespaced by module under App\Actions.
> We use Livewire + AlpineJS for the frontend and Pest for testing.
>
> Task: [your task here]
> ```

**Always run AI-generated code through the quality pipeline before committing.** Don't skip Pint, PHPStan, or tests because "the AI wrote it."

**Use AI to generate test cases.** It's one of the highest-ROI uses of AI in development.

> **💡 Test Generation Prompt Example**
> ```
> Generate Pest tests for the following action class. Cover:
> - Happy path
> - Edge cases
> - Failure / exception scenarios
>
> [paste your action class here]
> ```

**For complex Livewire components**, ask AI to propose the component split before writing code — what should be a child component, what state should lift up.

Commit AI-assisted code the same way you'd commit your own: clean, purposeful commits with clear messages.

---

## ✅ Code Quality Pipeline

Code quality is non-negotiable. Automated tooling handles style and analysis so that reviews can focus on logic and architecture.

### PHP / Laravel

#### Laravel Pint — Code Style

Zero-config code style fixer. PSR-12 + Laravel preset. **Run before every commit.**

```bash
./vendor/bin/pint
```

To check without fixing:
```bash
./vendor/bin/pint --test
```

---

#### Larastan (PHPStan) — Static Analysis

Catch bugs before runtime. Aim for **Level 5** minimum; push toward **Level 8+** on greenfield projects.

```bash
./vendor/bin/phpstan analyse
```

`phpstan.neon` baseline config:
```neon
includes:
    - vendor/larastan/larastan/extension.neon

parameters:
    paths:
        - app
    level: 6
```

---

#### Pest PHP — Testing

Our preferred test framework. Expressive, minimal boilerplate, pairs beautifully with Laravel.

```bash
./vendor/bin/pest
```

Use **Pest Architecture Tests** to enforce your own conventions as runnable specs:

```php
arch('actions are invokable')
    ->expect('App\Actions')
    ->toBeInvokable();

arch('models do not contain business logic')
    ->expect('App\Models')
    ->not->toHavePublicMethodsBesides([
        'relationships', 'scopes', 'casts', 'fillable'
    ]);
```

> **💡 Tip:** Architecture tests are a great safety net for a small team. They encode your conventions so that violations are caught automatically — no manual code review needed for these.

---

#### Rector — Automated Refactoring

Automated PHP upgrades and refactoring. Run periodically — not on every commit.

```bash
# Dry run first — always
./vendor/bin/rector process --dry-run

# Apply changes
./vendor/bin/rector process
```

---

### JavaScript / Frontend

- **[ESLint](https://eslint.org/)** — Linting for JS and AlpineJS logic
- **[Prettier](https://prettier.io/)** — Code formatting; configure with the Tailwind class sorting plugin
- **[Tailwind CSS IntelliSense](https://tailwindcss.com/docs/editor-setup)** — Install in your editor; catches class typos early

---

### Git Hooks — Automate the Pipeline

Use **[CaptainHook](https://github.com/captainhookphp/captainhook)** (PHP-native) or **[Husky](https://typicode.github.io/husky/)** to enforce checks at commit time.

```
pre-commit  →  Pint, ESLint, Prettier
pre-push    →  PHPStan, Pest
```

> **💡 Tip:** This ensures no one accidentally pushes code that fails analysis or breaks tests — even when using AI-generated code that looks correct at a glance.

---

### CI/CD

Run the full pipeline on every pull request via **[GitHub Actions](https://github.com/features/actions)**.

```yaml
# .github/workflows/ci.yml
name: CI

on: [push, pull_request]

jobs:
  quality:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install Dependencies
        run: composer install --no-interaction
      - name: Pint (Style Check)
        run: ./vendor/bin/pint --test
      - name: PHPStan (Static Analysis)
        run: ./vendor/bin/phpstan analyse
      - name: Pest (Tests)
        run: ./vendor/bin/pest
```

> **⚠️ Rule:** A PR cannot be merged if CI is red. No exceptions.

---

## 💻 Codebase

### General

- Write comments for **context and why**, not for what. The code says what; the comment says why.

> **✅ Good Comment**
> ```php
> // We store the raw payload here because the third-party webhook signature
> // validation requires the exact original bytes — parsing it first would
> // alter whitespace and break the HMAC check.
> $rawPayload = $request->getContent();
> ```
>
> **❌ Bad Comment**
> ```php
> // Get the content of the request
> $rawPayload = $request->getContent();
> ```

- If your code needs comments to explain *what* it does, refactor it until it doesn't.
- One commit per task. Each commit represents a feature or a fix — nothing more.
- Never mix formatting changes with logic changes in a commit. Formatting gets its own commit.
- Always store **UTC timestamps**. You may also store a timezone offset, but UTC is mandatory.
- Avoid magic strings and numbers. Wrap them in constants, enums, or class properties.
- Use **Enums** to enforce strong typing wherever you have a fixed set of values.
  > **✅ Good — Enum**
  > ```php
  > enum OrderStatus: string {
  >     case Pending  = 'pending';
  >     case Shipped  = 'shipped';
  >     case Delivered = 'delivered';
  > }
  >
  > $order->status = OrderStatus::Shipped;
  > ```
  >
  > **❌ Bad — Magic String**
  > ```php
  > $order->status = 'shipped'; // What are the valid values? Nobody knows.
  > ```
- Be generous with namespaces. A rule of thumb: wait until you have at least two files in a module before creating a namespace, unless expansion is certain.
- Use a text diff tool when facing "not found" errors that look correct. It will save you hours. [A Lesson Based on Pain](http://github.com/DevForce-141/Chamber-Of-Wisdom/blob/main/honest-work/solving-file-import-errors-quickly.md)

---

### UI / Frontend

- If CSS can do it, do it in CSS.
- Prefer JS over CSS only when the CSS solution is disproportionately complex.
- **Prefer data attributes over CSS classes for DOM manipulation.**

> **💡 Why?**
>
> CSS classes get tweaked over time for styling reasons. If you use them for JS hooks too, you'll be scared to remove or rename them. Data attributes are stable by nature.
>
> ```html
> <!-- ✅ Good — data attribute for JS hook -->
> <button data-action="submit-order">Place Order</button>
>
> <!-- ❌ Bad — CSS class doubling as JS hook -->
> <button class="btn-primary submit-order">Place Order</button>
> ```

---

### Laravel

- **Create New Project with Code Quality Preconfigured** using our starter kit; Use command ``laravel new ProjectName --using=devforce141/code-quality-starter-kit``
  > Note: Using the starter kit has the benefit of using it in latest way as its updated!
- **Do not use Repository Pattern** unless absolutely necessary. Eloquent Models already act as repositories. The exception is when building a tech-agnostic layer to allow swapping implementations via contracts.

- **Prefer the Action Pattern** for all tasks. Use [Laravel Actions](https://www.laravelactions.com/). Namespace actions by module.

> **💡 Action Class Example**
> ```php
> namespace App\Actions\Order;
>
> use Lorisleiva\Actions\Concerns\AsAction;
>
> class PlaceOrder
> {
>     use AsAction;
>
>     public function handle(Cart $cart, User $user): Order
>     {
>         // ...
>     }
> }
> ```
>
> This same class can now be used as a controller, job, command, or listener — without creating separate wrapper classes for each.

- Services and Actions can coexist. Keep shared/configuration-level logic in services; specific operations go into actions.
- It's acceptable to write 5–10 lines directly in a controller. Avoid over-engineering small things.
- Use **Form Requests** for long or complex validation. A **Validation Service** is a good middle ground as a project scales.
- Use **JSON Resources** only when you need to send a model as a JSON response. Don't pre-create them speculatively.
- Keep controllers slim. They receive the request, delegate, and return the response.
- **Centralise all Session interactions** (GET, SET, FORGET) in one place. Hundreds of lines is fine — you'll thank yourself when refactoring.
- **Centralise all Cache interactions** (GET, SET, FORGET) in one place. Same reasoning.
- **Write tests early.** Run the full test suite after every task. Green tests mean confidence. Confidence means speed.
- Comply with **PSR standards** as much as possible.
- Follow [Spatie's Laravel guidelines](https://spatie.be/guidelines/laravel-php) as a baseline.

---

### Livewire

- Set up one generic layout that all Livewire components can use. Create additional layouts only when genuinely needed, extending the base.
- Prefer **PHP Attributes** for simple, non-dynamic values.

```php
#[Title('Dashboard')]
#[Layout('layouts.app')]
class Dashboard extends Component
{
    // ...
}
```

- Keep layout files clean and consistent — they are the backbone of every view.
- Split components thoughtfully. If a component is doing too much, it's probably two components.

> **💡 Tip:** Use AI to propose component splits when you're unsure. Describe what your component does and ask: *"How would you split this into smaller Livewire components? What state should lift up?"*

---

# 👩‍💻 Useful Resources

- **[Laracasts](https://laracasts.com/)** — Learning new things in the Laravel ecosystem
- **[Spatie Guidelines](https://spatie.be/guidelines/laravel-php)** — Our baseline for Laravel/PHP conventions
- **[Laravel Actions](https://www.laravelactions.com/)** — Core to our action pattern
- **[Pest PHP](https://pestphp.com/)** — Our test framework of choice
- **[Larastan](https://github.com/larastan/larastan)** — Static analysis for Laravel
- **[Laravel Pint](https://laravel.com/docs/pint)** — Zero-config code style fixer
- **[Rector](https://getrector.com/)** — Automated refactoring and PHP upgrades
- **[CaptainHook](https://github.com/captainhookphp/captainhook)** — PHP-native Git hooks

---

> 📝 **This is a living document.** When you encounter a situation not covered here, or where a guideline proved wrong in practice, raise it. We update the guidelines, not just the code. Moreover, the Code Reviews & AI part is new here and actively being explored; Once stabilized, proper docs will be written regarding it here!
