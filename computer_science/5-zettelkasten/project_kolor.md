### Meta
2024-09-23 17:16
**Tags:** [[projects]]
**State:** #pending

### Project overview
#### Objective
- Create a web application that helps choosing colors for your web applications based on color themes, and ready-to-use output comprising of either CSS, SCSS or LESS variables.

#### Key Features
- Color palette.
- Color markers based on color schemes.
- Code output (CSS, SCSS, LESS).
- Bookmarks.

#### Technology Stack
- **Core**
	- HTML
	- CSS
	- JavaScript / TypeScript
	- SQL.
- **Tools**
	- React
	- Vite
	- NodeJS
	- AJAX ??
	- PostgreSQL ?
	- sequelize ??
	- pg
	- Express
	- Nodemon
	- Dotenv
	- cors
	- jsonwebtoken
	- bcryptjs
	- morgan
	- OAuth
	- Mocha
	- Docker
	- Github Actions
	- Render
	- Netlify

### Planning

#### Project Timeline

- [ ] **Phase 0 – Research**
	- Understand the tools required to complete the project.
	- Understand the system design of the application.
	- Collect source material with simple examples.
- [ ] **Phase 1 – List User Stories**
	- Create user stories for all elements and behaviors of the application.
- [ ] **Phase 2 – Translate User Stories into Features**
	- Ensure each user story is clearly translated into a unique feature.
- [ ] **Phase 3 – Wireframing **
	- Use Excalidraw to lay out the basic architecture of the main application.
- [ ] **Phase 4 – UI/UX
	- Search ideas.
	- Write down a concise description of the user experience.
	- Create a style guide. Sure would be useful to have this tool in handy, eh?
- [ ] **Phase 5 – Frontend Architecture**
	- Research frontend architecture models.
	- Study the elected architecture.
	- Figure out state management test.
- [ ] **Phase 6 – Backend Architecture**
	- Research backend architecture models.
	- Study the elected architecture.
- [ ] **Phase 7 - Database Design**
	- Research database design using PostgreSQL.
	- Design cluster to fit the needs of the application.
- [ ] **Phase 8 – API Design**
	- Research API structures.
	- Look into Swagger editor.
- [ ] **Phase 9 – Code Structure**
	- Create a mock-up of the future file-tree.
- [ ] **Phase 10 –  Dependencies**
	- List all the dependencies required to complete the project and a brief description of what they do.
	- Peruse their documentation.
- [ ] **Phase 11 – Frontend Component Design**
	- List all the components required to build the app.
	- Explain what each component must achieve.
	- Pseudo-code them components.
- [ ] **Phase 12 – State management**
	- Figure out how to integrate state management into the core logic of the app.
- [ ] **Phase 13 – Backend API Endpoint Design**
	- Structure API endpoints.
- [ ] **Phase 14 – Backend Auth Considerations**
	- Design authentication system.
	- Design authorization system.
	- Consider the what integrating authorization (admin account) implies (changes to state, unique components, permissions, etc.)
- [ ] **Phase 15 – Database Management**
	- Design DB schema.
- [ ] **Phase 16 – Testing Design**
	- Unit
	- Integration
	- End-to-end?
- [ ] **Phase 17 – Revisit Architecture**
	- Refine wireframes.
	- Write a step-by-step detailed implementation guide.
- [ ] **Phase 18 - Branching Strategy**
	- Create a branching strategy before setting up the project.
	- Stick to it whenever you add/modify a feature.
- [ ] **Phase 19 - Initialize Project**
	- Create the Github repository with license and README.
	- Clone git repository into the `/repos` directory.
	- Create basic repository structure → `index.html`, `style.css`, `app.js`, and `src` directory.
- [ ] **Phase 20 - Create core app functionality, without a UI**
	- A function that takes in an input and returns a `string`.
	- A function that translates the return `string` into one of three formats:
		- CSS variable
		- SCSS variable
		- LESS variable
	- 1234

#### Research
- [x] 2024-09-26 21:10 – completed research on [[color_theory]]
- [x] 2024-09-26 22:08 – research how to develop a REST API with Go.
- [x] Learn how to use tmux, dummie!
- [ ] 2024-09-30 13:01 – study the ExpressJS documentation.

#### User Stories
- As a user, I want to be able to pick a color.
- As a user, I want to be able to convert the picked color into various formats.
- As a user, I want to be able to select a color harmony.
- As a user, I want to be able to visualize how the selected color harmony might look on some boilerplate application.
- As a user, I want to obtain said color harmony in a CSS (and derivatives) variable format.
- As a user, I want to be able to copy the choice output to clipboard.
- As a user, I want to bookmark my color harmonies.
- As a user, I want to be able to see all my bookmarked harmonies.
- As a user, I want to be able to authenticate into the application.
- As a user, I want to understand how the application works.

##### Future development direction
- As a user, I want to be able to use this application in terminal.

#### Milestones
- Break the project into key achievements or deliverables.

### Design

#### Wireframes
- …

#### User Interface
 - Visuals

#### User Experience
- Objectives

#### Style Guide
- Set design standards for typography, colors, and other design elements.

### Architecture

#### Frontend
- **Model:** The model represents the data and the business logic of your application. It encapsulates data-related operations and ensures the integrity of your data. In our case, here we’ll have our SQL schema.

#### Backend
- Server-side logic, APIs, business logic.

#### Databes Design
- Defines the structure and relationships of the data models.

#### API Design / Integrations
- Plan how external services or data sources will be integrated.

### Development

#### Code Structure / File Organization
- Provides a guide for organizing project files and folders.

#### Dependencies / Libraries Used
- Lists external libraries or frameworks used in the project.

### Frontend Development
#### Components
- List components

#### State Management
- Choose tool.

### Backend Development

#### API Endpoints
- List

#### Authentication / Authorization
- List

### Database Management

#### Data Models / Schemas
- Examples…

#### Migrations
- …

### Testing

#### Unit Testing
- List tools.
- Examples.

#### Integration Testing
- List toosl.
- Examples.

#### End-to-End Testing
- Test the app from the user’s perspective, simulating real user interactions.

#### Test Automation
- Use tools to automatically run tests on new changes.

### Deployment

#### Environment Setup
- Do this.

#### Build and Deployment Process
- Do that.

#### Continuous Integration / continuous Deployment
- Thus do.

### Security

#### Auth
- Do this

#### Data Encryption
- This

#### Vulnerability Management
- This.

### Performance

#### Caching Strategies
- Like so.

#### Load Balancing
- Traffic

#### Speed Optimization
- Reduce load times (lazy loading, minimizing assets).

### Maintenance

#### Bug Tracking & Issue Resolution
- Something.

#### Regular Updates & Patches
- Stuff.

#### Refactoring
- DO!

### Analytics & Monitoring

#### User Analytics
- Track user interact.

#### Error Logging
- Somehow?

#### Performance Monitoring
- Perhaps.

### Version Control

#### Branching Strategy
- Gitflow

#### Git Workflows
- Contribution guidelines.

#### Version Releases / Tags
- Label and tag different versions or releases of the app.

### Documentation

#### Code Documentation
- JSDoc

#### API Documentation
- Details the structure and usage of the app’s API.

#### User Documentation / Tutorials
- Do that.

### README
- Provides an overview of the project, including setup instructions for developers.