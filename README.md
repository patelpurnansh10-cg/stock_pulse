# 📈 StockPulse

> A full stack stock market news & analysis platform built for students learning about the stock market.

![React](https://img.shields.io/badge/React-18-61DAFB?style=flat&logo=react)
![Node.js](https://img.shields.io/badge/Node.js-Express-339933?style=flat&logo=node.js)
![MongoDB](https://img.shields.io/badge/Database-MongoDB-47A248?style=flat&logo=mongodb)
![TailwindCSS](https://img.shields.io/badge/Styling-TailwindCSS-06B6D4?style=flat&logo=tailwindcss)

---

## 🎯 Problem Statement

Students learning about the stock market have no single platform where they can view live stock charts, read real market news, and discuss analysis with peers. StockPulse solves this by combining live stock data, real news headlines, and a student community — all in one beginner-friendly app.

---

## 💡 Solution

StockPulse is a full stack web application where students can:

- Track live NSE stock prices with interactive charts
- Read real stock market news fetched from NewsAPI
- Write and share their own stock analysis posts
- Build a personal watchlist of stocks they want to follow
- Track a virtual (paper trading) portfolio with live P&L
- Set price alerts on stocks they are watching

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | ReactJS, Tailwind CSS |
| State Management | Redux Toolkit |
| Routing | React Router DOM |
| Charts | Recharts |
| Backend | Node.js, Express.js |
| Database | MongoDB (Mongoose) |
| Auth | JWT (JSON Web Tokens) |
| Stock Data | yahoo-finance2 (npm) |
| News Data | NewsAPI.org |
| Notifications | react-hot-toast |

---

## ✨ Features

### 🏠 Homepage
- Hero section with app tagline and call-to-action buttons
- Trending NSE stocks strip with live price and % change (RELIANCE, TCS, INFY, HDFC, WIPRO, ICICI)
- Preview of latest 3 community analysis posts
- Fully responsive Navbar with dark/light mode toggle

### 🔑 Authentication
- Signup page with name, email, password and full validation
- Login page with JWT token stored in localStorage
- Redux `authSlice` for global auth state
- Protected routes — redirects to /login if not authenticated
- Logout clears token and resets state

### 📰 News Dashboard
- **Two tabs:** Real News (from NewsAPI) and Community Analysis (from MongoDB)
- Debounced search bar (500ms) — filters posts by title or content
- Sector filter buttons — All / IT / Banking / Pharma / Auto / Energy
- Sort dropdown — Latest first / Oldest first
- Beginner-friendly tag filter — students can find beginner posts easily
- Backend pagination — 10 posts per page with limit & skip in MongoDB
- Loading spinner during API calls

### 📈 Stock Charts & Data
- Live price chart using Recharts AreaChart
- Green fill when price is up, red fill when price is down
- Time range selector — 1D / 1W / 1M / 3M / 1Y
- Auto-refresh every 60 seconds using `useEffect` + `setInterval`
- Stock detail page — symbol, company name, current price, % change, OHLC data
- Stock-specific real news from NewsAPI shown below the chart
- Stock search bar to navigate to any NSE stock by symbol
- Trending stocks section on homepage and stocks page

### 💬 Community Posts & Analysis
- Browse all posts without login (open access)
- Create post with title, content, stock symbol, sector, beginner-friendly toggle (login required)
- Edit own post — pre-filled form (login required, own post only)
- Delete own post — with confirmation dialog (login required, own post only)
- Post detail page with full content, author, date, sector tag
- Add comment on any post (login required)
- Delete own comment (login required, own comment only)

### ⭐ Watchlist
- Add any stock to personal watchlist via star button (login required)
- View watchlist page with live prices fetched on load
- Remove stock from watchlist instantly
- Click any watchlist stock → opens stock detail page with live chart

### 💼 Portfolio Tracker (Paper Trading)
- Virtual buy any stock at current price with a quantity
- Portfolio dashboard at /portfolio showing all holdings
- Live P&L calculated: (currentPrice - buyPrice) × quantity
- Green P&L for profit, red for loss
- Portfolio allocation pie chart using Recharts PieChart
- Remove/sell holding from portfolio

### 🔔 Stock Price Alerts
- Set a price alert on any stock — "Alert me when TCS crosses ₹4000"
- Choose condition: Above or Below a target price
- On login/dashboard load, backend checks alerts against live prices
- Toast notification fires when an alert is triggered: "🔔 TCS crossed ₹4000!"
- View and delete all active alerts from the Profile page

### 👤 Profile Page
- Displays user info: name, email, member since, total posts, total comments
- My Posts tab — all posts by the user with Edit and Delete options
- My Watchlist tab — watchlist accessible directly from profile
- My Alerts tab — all active price alerts with delete option

### ⚙️ App-Wide
- Dark / Light mode toggle — persisted in localStorage, Tailwind `dark:` classes
- Fully responsive — works on mobile, tablet, and desktop
- Loading states on every API call — never shows a blank screen
- Toast notifications — success/error feedback using react-hot-toast
- Error handling — try/catch on all API calls, user-friendly error messages
- Back to top button — appears on scroll, smooth scroll to top
- 404 Not Found page with back to home button

---

## 📁 Project Structure

```
stockpulse/
├── client/                        # React Frontend
│   ├── public/
│   └── src/
│       ├── components/
│       │   ├── Navbar.jsx
│       │   ├── StockChart.jsx
│       │   ├── NewsCard.jsx
│       │   ├── PostCard.jsx
│       │   ├── CommentList.jsx
│       │   ├── Pagination.jsx
│       │   ├── SectorFilter.jsx
│       │   ├── WatchlistCard.jsx
│       │   ├── PortfolioCard.jsx
│       │   ├── AlertCard.jsx
│       │   ├── BackToTop.jsx
│       │   └── PrivateRoute.jsx
│       ├── pages/
│       │   ├── Home.jsx
│       │   ├── Login.jsx
│       │   ├── Signup.jsx
│       │   ├── NewsDashboard.jsx
│       │   ├── StocksPage.jsx
│       │   ├── StockDetail.jsx
│       │   ├── Community.jsx
│       │   ├── PostDetail.jsx
│       │   ├── CreatePost.jsx
│       │   ├── EditPost.jsx
│       │   ├── Watchlist.jsx
│       │   ├── Portfolio.jsx
│       │   ├── Profile.jsx
│       │   └── NotFound.jsx
│       ├── store/
│       │   ├── index.js
│       │   ├── authSlice.js
│       │   ├── themeSlice.js
│       │   ├── postSlice.js
│       │   └── stockSlice.js
│       ├── hooks/
│       │   ├── useDebounce.js
│       │   └── usePagination.js
│       ├── utils/
│       │   ├── api.js             # Axios instance with JWT interceptor
│       │   └── validators.js
│       └── App.jsx
│
└── server/                        # Node.js Backend
    ├── models/
    │   ├── User.js
    │   ├── Post.js
    │   ├── Comment.js
    │   ├── Watchlist.js
    │   ├── Portfolio.js
    │   └── Alert.js
    ├── routes/
    │   ├── auth.js
    │   ├── posts.js
    │   ├── comments.js
    │   ├── stocks.js
    │   ├── news.js
    │   ├── watchlist.js
    │   ├── portfolio.js
    │   └── alerts.js
    ├── middleware/
    │   └── authMiddleware.js
    ├── controllers/
    │   ├── authController.js
    │   ├── postController.js
    │   └── stockController.js
    ├── .env
    └── index.js
```

---

## 🗄️ MongoDB Collections

| Collection | Key Fields |
|---|---|
| `users` | name, email, password (hashed), createdAt |
| `posts` | title, content, sector, stockSymbol, isBeginnerFriendly, author (ref), createdAt |
| `comments` | text, postId (ref), author (ref), createdAt |
| `watchlists` | userId (ref), symbol, addedAt |
| `portfolios` | userId (ref), symbol, buyPrice, quantity, buyDate |
| `alerts` | userId (ref), symbol, targetPrice, condition (above/below), triggered |

---

## 🔌 API Endpoints

### Auth — `/api/auth`
| Method | Route | Description | Auth |
|---|---|---|---|
| POST | `/register` | Create new user account | No |
| POST | `/login` | Login and receive JWT token | No |
| GET | `/me` | Get logged-in user info | Yes |

### Posts — `/api/posts`
| Method | Route | Description | Auth |
|---|---|---|---|
| GET | `/` | Get all posts (filter, sort, paginate) | No |
| GET | `/:id` | Get single post | No |
| POST | `/` | Create new post | Yes |
| PUT | `/:id` | Edit own post | Yes |
| DELETE | `/:id` | Delete own post | Yes |

### Comments — `/api/comments`
| Method | Route | Description | Auth |
|---|---|---|---|
| GET | `/post/:postId` | Get all comments for a post | No |
| POST | `/post/:postId` | Add comment to post | Yes |
| DELETE | `/:id` | Delete own comment | Yes |

### Stocks — `/api/stocks`
| Method | Route | Description | Auth |
|---|---|---|---|
| GET | `/:symbol/history` | Get historical OHLC data | No |
| GET | `/:symbol/quote` | Get current price & % change | No |
| GET | `/trending` | Get prices for trending stocks | No |

### News — `/api/news`
| Method | Route | Description | Auth |
|---|---|---|---|
| GET | `/real` | Fetch headlines from NewsAPI | No |
| GET | `/real?q=TCS` | Stock-specific headlines | No |

### Watchlist — `/api/watchlist`
| Method | Route | Description | Auth |
|---|---|---|---|
| GET | `/` | Get user's watchlist | Yes |
| POST | `/` | Add stock to watchlist | Yes |
| DELETE | `/:symbol` | Remove stock from watchlist | Yes |

### Portfolio — `/api/portfolio`
| Method | Route | Description | Auth |
|---|---|---|---|
| GET | `/` | Get user's portfolio with live P&L | Yes |
| POST | `/` | Buy (add) a stock to portfolio | Yes |
| DELETE | `/:id` | Sell (remove) a holding | Yes |

### Alerts — `/api/alerts`
| Method | Route | Description | Auth |
|---|---|---|---|
| GET | `/` | Get all user alerts | Yes |
| POST | `/` | Create new price alert | Yes |
| GET | `/check` | Check alerts against live prices | Yes |
| DELETE | `/:id` | Delete an alert | Yes |

---

## 🚀 Getting Started

### Prerequisites
- Node.js v18+
- MongoDB Atlas account (free tier)
- NewsAPI key — free at [newsapi.org](https://newsapi.org)

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/stockpulse.git
cd stockpulse
```

### 2. Setup the backend
```bash
cd server
npm install
```

Create a `.env` file in the `server/` folder:
```env
MONGO_URI=your_mongodb_atlas_connection_string
JWT_SECRET=your_secret_key_here
NEWS_API_KEY=your_newsapi_key_here
PORT=5000
```

Start the backend server:
```bash
node index.js
```

### 3. Setup the frontend
```bash
cd client
npm install
npm start
```

The app will open at `http://localhost:3000`

---

## 🧩 React Hooks Used

| Hook | Where Used |
|---|---|
| `useState` | Form inputs, loading states, pagination, range selector |
| `useEffect` | API calls on mount, auto-refresh interval, scroll listener |
| `useRef` | Debounce timer on search bar |
| `useContext` | Auth context, theme context |
| `useNavigate` | Redirect after login/logout/post create |
| `useParams` | Get stock symbol and post ID from URL |

---

## 📦 NPM Packages

### Frontend
```
react-router-dom    → client-side routing
axios               → HTTP requests
redux               → state management
@reduxjs/toolkit    → simplified Redux
react-redux         → connect Redux to React
recharts            → stock charts, portfolio pie chart
react-hot-toast     → toast notifications
tailwindcss         → styling
```

### Backend
```
express             → web framework
mongoose            → MongoDB ODM
cors                → cross-origin requests
dotenv              → environment variables
bcryptjs            → password hashing
jsonwebtoken        → JWT auth
yahoo-finance2      → live NSE stock data
axios               → NewsAPI calls
```

---

## 🎓 Hackathon Requirements Coverage

| Requirement | How It's Covered |
|---|---|
| React Router | 12+ pages with nested and protected routes |
| `useState` | Forms, loading, pagination, range selector |
| `useEffect` | API calls, auto-refresh, scroll listener |
| `useRef` | Debounce timer on search bar |
| `useContext` | Auth and theme context |
| Redux / Context API | Redux Toolkit with authSlice, themeSlice, postSlice |
| Authentication | JWT + bcrypt + localStorage + protected routes |
| Dark / Light Mode | Redux themeSlice + Tailwind `dark:` + localStorage |
| Search + Filter + Sort | News dashboard with all three applied |
| Debouncing | 500ms debounce on search bar using useRef |
| Pagination | Backend limit/skip + frontend page UI |
| CRUD | Full create/read/update/delete on posts and comments |
| REST APIs | Express routes for all features |
| Form Validation | Signup, login, create post, alerts |
| Responsive UI | Tailwind sm: md: lg: breakpoints throughout |
| Error Handling | try/catch on all API calls + user-friendly messages |

---

## 👨‍💻 Developer

**Name:** [Your Name]  
**College:** [Your College Name]  
**Department:** [Your Department]  
**Year:** [Your Year]

---

## 📄 License

This project was built for educational purposes as part of a Full Stack Hackathon.