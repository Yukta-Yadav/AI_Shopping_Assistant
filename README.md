# 🛒 AI Shopping Assistant

An LLM-powered shopping assistant that helps users search for products using natural language, check ratings, discover products from images, and place orders after user confirmation.

<img width="1863" height="842" alt="image" src="https://github.com/user-attachments/assets/629468d7-cddc-41df-b129-42a908167b84" />


## ✨ Features

* 🔎 **Natural-language product search** — Search using product name, category, price, and organic filters.
* ⭐ **Rating-based filtering** — Retrieves average product ratings and review counts from SQLite.
* 🖼️ **Image-based product discovery** — Uses a vision LLM to extract product attributes from uploaded images and search the product database.
* 🛍️ **User-confirmed checkout** — Places an order only after explicit user confirmation.
* 💬 **Conversational interface** — Streamlit chat interface with session-based conversation history.
* 🔧 **LLM tool calling** — Uses LangChain tools for product search, ratings, image analysis, and checkout.

## 🏗️ Architecture

```text
                    ┌──────────────────┐
                    │       User       │
                    │ Text / Image     │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │   Streamlit UI   │
                    │     app.py       │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │  LangChain Agent │
                    │   Qwen + Groq    │
                    └────────┬─────────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
       Search Products   Get Rating      Checkout
              │              │              │
              └──────────────┼──────────────┘
                             ▼
                    ┌──────────────────┐
                    │  SQLite Database  │
                    │    store.db      │
                    └──────────────────┘

       Image Upload
            │
            ▼
      Vision LLM
            │
            ▼
    Product Attributes
            │
            ▼
     Product Search
```

## 🧰 Tech Stack

| Technology | Purpose                            |
| ---------- | ---------------------------------- |
| Python     | Core development                   |
| LangChain  | Agent and tool orchestration       |
| Qwen       | LLM and vision model               |
| Groq       | LLM inference                      |
| SQLite     | Product, review, and order storage |
| Streamlit  | Interactive web interface          |

## 🔧 Agent Tools

The shopping agent uses four tools:

### `search_products()`

Searches the SQLite product database using:

* Product keywords
* Maximum price
* Organic/non-organic preference

### `get_rating()`

Retrieves:

* Average product rating
* Number of reviews

### `describe_product_image()`

Uses the vision LLM to extract product information such as:

* Product type
* Search query
* Organic status
* Description

### `checkout()`

Creates an order in the SQLite database after the user explicitly confirms the selected product.

## 🗄️ Database

The project uses SQLite with three main tables:

```text
products
├── id
├── name
├── category
├── price
├── description
└── is_organic

reviews
├── id
├── product_id
├── rating
├── reviewer_name
└── review_text

orders
├── id
├── product_id
├── product_name
├── price
└── ordered_at
```

## 💬 Example Queries

```text
Find organic honey under $20 with a rating above 4.5.
```

```text
I want to buy this product.
```

Users can also upload a product image and ask the assistant to find relevant products in the database.

## 🚀 Setup

### 1. Clone the repository

```bash
git clone https://github.com/Yukta-Yadav/ai-shopping-assistant.git
cd ai-shopping-assistant
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Create `.env`

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key
```

### 4. Run the application

```bash
streamlit run app.py
```

The application will open in your browser.

## 📌 Project Highlights

* Built an LLM-powered shopping agent using **LangChain and Qwen**.
* Implemented **4 custom tools** for product search, rating retrieval, image analysis, and checkout.
* Integrated **SQLite** for product, review, and order management.
* Added **vision-based product discovery** through image uploads.
* Built an interactive **Streamlit** interface for conversational shopping.

## 🔮 Future Improvements

* Semantic/vector-based product search
* Real-time inventory availability
* User authentication and personalized recommendations
* Product embeddings for more advanced image/product similarity
* Integration with real payment and e-commerce APIs
* Automated evaluation of search and recommendation quality

B.Tech Computer Science & Engineering (AI)
IGDTUW
