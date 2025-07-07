## Hi there 👋

# 🙋‍♀️ Introduction?
DevForce 141 is a special task force of developers. Atleast, this is what we like to think of it. We are all friends who are joining up together to make great stuff with a hope that the stuff will help us to even greater stuff :)
## Our Tech Stack
We love Laravel and it's ecosystem. Here's a list of all the tech we work with:

### Languages
- PHP
- JavaScript
- C# (Only When PHP & JS can't be used for one reason or another)
- Java (Only When PHP & JS can't be used for one reason or another)

### Markup/Non-Programming Languages
We don't want ``definitions`` wars, hence we're putting them here.
- HTML
- CSS
- SQL
- XML
- JSON

### Frameworks
- Laravel
- Tailwind CSS
- Bootstrap

### Libraries
- Livewire
- AlpineJS
- Flux UI
- ReactJS
- VueJS
- jQuery

### CMS/Builds
- WordPress
- Shopify

### Databases
- MySQL
- PostgresSQL
- MongoDB

### Clouds
- AWS
- Azure
- Digital Ocean

# 🌈 Guidelines for Requirements Providers/Clients
These guidelines will make the life slightly easier for everyone involved.

- If you're sharing something early stage, be sure to mention that it's early stage and acknowledge it's shortfalls. This will avoid lot of lurking which costs time and often creates confusion.
- Be explicit as much as you can. The more explicit you're, the more chances that your message is being received as intended.
- Don't assume that others will magically figure out. Give the context and forward knowledge/info to your best. For example, if you're providing a database dump, just mention the DBMS name and it's version.

# 🌈 Development Guidelines
We like to keep understand the system which we develop and we pay very good attention to semantics and naming which in turn allows us to stay clear of confusions and maintain a clean codebase. We've guidelines which span across different phases of project, not just codebase only.
## Understanding Project
- Identify entities in any project.
- Name the entities in a way which is closer to what they reflect/mean. In other words, name them semantically. The more specific, the better. For example, if you're working on a crypto project where users initiate mining and you consider it as ``session``; It's better to name it as ``MiningSession`` because ``Session`` is generic in computing/software and is often core part of whatever language/framework, you're working in.
- Identify ambiguous requirements and missing bits. There are always many.
- When in doubt, bring it up and clear it out. It'll bite and hurt down the road, otherwise.

## Communication
As communication is important in every aspect of life, it's important here too. Often Communication is the deciding factor between a good and bad outcome.

- Please re-read/review whatever you write. Remove any typos and reconsider that your message conveys the message that you intend.
- Try to keep each sentence, clause limited to 1 topic. Don't jam up multiple things in one!
- Use Lines breaks effectively to reduce the clutter, add breathing space and make your text easy on the eyes.
- Proper punctuation is the diffference between confusion and clarity. Make extensive use of comma ``,``, semicolon ``;``, fullstop ``.``, double quotes ``""``.
- Wrap anything 100% as it is in double quotes. For example, referring to some button label in UI.

## Codebase
### Programming
- Use comments for adding context and ``WHY`` the code is written in a certain way. When you'll come back after weeks or months, the code will be there in file but the ``context`` and ``WHY`` will not be there unless you wrote it in comments.
- If you have to write comments to explain your code, you're doing it wrong. Adjust your code in a way that it doesn't need comments to explain what it does!
- Try to do 1 commit per each task. This keeps the git clean, each commit means a feature or fix. Whenever you'll have to read the commits, life will be easy!
- If you're doing a task and about to commit it, don't run formatter OR commit (in case you ran formatter) and there are 69420 lines changed, which are all formatting changes. If you must do it, do it in a separate commit with only formatting changes. A commit which mixes up so many formatting changes alongside some code changes, is hard to navigate/read in times of need.
- Always store UTC timestamps. You may store timezone offset or another timezone timestamp but you must store UTC as well. It's a good practice and will help you when you run into situations.
- If you're having an issue where it seems you've written the code correctly but the result is complaining about something not found etc (usually typos), please reach for a text diff tool. It'll highlight and may save your hours. [A Lesson Based on Pain](http://github.com/DevForce-141/Chamber-Of-Wisdom/blob/main/honest-work/solving-file-import-errors-quickly.md)
- Be Generous about namespaces, they don't incurr rent. Grouping your code in relevant directories/namespaces like a module keep things clean. There's a judgement call to make; If you know that you're starting off a module which is going to expand (with very high certainty), you can create namespace; Otherwise, just keep it in the main namespace/directory. Another approach is to always house it in main, until you've at least two files in a module.
- Avoid Magic Strings and Numbers in your codebase. Wrap them in constants, enums or data properties of class. It's a seemingly small thing but it has huge impact.
- Use Enums when you need to enforce strong typing.
  
### UI/Frontend
- Anything which CSS can do it, do it via CSS.
- Prefer JS over CSS only when CSS solution is very complicated!
- Prefer using data attributes over css classes for dom manipulation. Otherwise, you'll be shit scared to remove classes from elements because you fear that it'll break some interactivity! CSS classes are something which you've to tweak over time for different reasons.

### Laravel
- Do not use Repository Pattern unless it's absolutely necessary. Eloquent Models already act like Repository.
- Prefer Action Pattern to wrap every action/task in its class. It's highly recommended to namespace them based on the module. Use [Laravel Actions](https://www.laravelactions.com/) package for this.
- Writing action classes gives the advantage of invoking that action as controller, job, command, listener etc. Otherwise, you would have to create job, command etc which would be just wrapper around your actual code.
- You can use Services and Actions in same project. In such case, keep the configuration level and common code within a service and each specific act can be wrapper in an action.
- It's okay to sometimes break your convention to reduce code navigation. For example if you have to write 5-10 lines in controller, you don't need an action or service there. It's okay.
- If validation is long or advanced, then a form request should be used. Otherwise, validation logic can be kept in controller/action. Another option would be to create a single Validation Service that contains code for all validations.
- JSON resources are used to seamlessly convert models to JSON responses. Models that don't require to be sent as JSON, may not have the resources. Do not create JSON resource until you need it.
- Controllers should handle requests and should be slim. They should do minimal things and act as really the controllers, delegating the tasks to other part of application, taking the output and eventually sending the response back to the requester/caller.
- Purpose of Seeder/Factories is to have minimal state of application which is ready to use interactively.
- Wrap all your interactions (GET, SET, FORGET) with Session in a central place. It's okay for it to be hundreds of line long. This way, you'll always have a single place to check when you're refactoring.
- Wrap all your interactions (GET, SET, FORGET) with Cache in a central place. It's okay for it to be hundreds of line long. This way, you'll always have a single place to check when you're refactoring.
- Testing is very important and it should be done early on. It'll pay off with future development. In an idea world, we run test suite after every task and the tests should be green; giving us the confidence that we didn't break anything.
- Comply with PSR standards as much as possible for PHP.
- Spatie has done pretty good and we tend to follow their [guidelines](https://spatie.be/guidelines/laravel-php) when it comes to Laravel ecosytem codebases.

### Livewire
- Setup one generic enough layout that all livewire components can use. If you need more variations, you can make relatively more specific layouts which extend the common layouts.
- Prefer PHP Attributes for simpler values (non-dynamic OR Computation based), for example ``#[Title], #[Layout]``.
- Strive for consistency, especially in your layout files as they'll be at the backbone of all your views. Make sure they are sensible and decently written.

# 👩‍💻 Useful Resources
- [Laracasts](https://laracasts.com/) (Good for Learning New stuff)
