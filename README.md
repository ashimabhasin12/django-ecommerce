# Django E-Commerce Platform

**A full-stack shopping platform with Django, customer accounts, order management, and experimental computer-vision experiences.**

**Repository:** https://github.com/ashimabhasin12/django-ecommerce  
**Status:** Development / portfolio project  
**Primary stack:** Python ┬╖ Django ┬╖ SQLite ┬╖ HTML ┬╖ CSS ┬╖ JavaScript

> **Development status:** The repository contains working application structure and a number of implemented or experimental workflows. A successful local Django system check has been reported, but a complete end-to-end test of every feature has not been established. The checkout flow should **not** be treated as a real payment integration or as production-ready.

## Contents

- [Project overview](#project-overview)
- [Objectives](#objectives)
- [Features](#features)
- [Architecture](#architecture)
- [Technology stack](#technology-stack)
- [Repository structure](#repository-structure)
- [Data model](#data-model)
- [Getting started](#getting-started)
- [Application routes](#application-routes)
- [How the workflows fit together](#how-the-workflows-fit-together)
- [Experimental features](#experimental-features)
- [Configuration and security](#configuration-and-security)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)
- [Screenshots and demo](#screenshots-and-demo)
- [Roadmap](#roadmap)
- [Acknowledgements and attribution](#acknowledgements-and-attribution)

## Project overview

Django E-Commerce is a web application exploring the design and implementation of a modern online shopping experience. It brings together a product catalogue, customer authentication, shopping cart, checkout and order records, customer reviews, wishlists, and supporting customer-service pages.

Alongside the conventional store workflow, the repository explores interactive additions such as product recommendations based on search history, community features, camera-based interfaces, virtual try-on, virtual lipstick, and voice-chatbot components. These are **experimental modules**; some may require additional configuration, assets, permissions, or debugging.

The application uses Django views and templates to connect the web interface to a relational data model. SQLite is configured for local development. The source is organized around a primary `store` app, with additional `chatbot` and `chatbox` directories.

This repository is intended as a software engineering and portfolio project, not a deployed commercial storefront.

## Objectives

The project explores several practical development goals:

1. Design an end-to-end Django web application with structured URLs, views, templates, and database models.
2. Model relationships among products, categories, customers, orders, and order items.
3. Support account-based shopping interactions such as carts, wishlists, and reviews.
4. Build product discovery through categories, search, and filtering.
5. Experiment with richer interfaces using computer vision, recommendations, and conversational features.
6. Practice maintainability, dependency management, secure configuration, and Git-based version control.

## Features

### 1. Product discovery and catalogue

- Storefront with product and category data loaded through Django models.
- Category-specific product pages and product-detail views.
- Search and product-filtering routes.
- Product attributes including title, description, price, color, availability, and images.
- Product-related recommendation logic using recent search history for authenticated users.

The models and routes establish these capabilities; the appearance and exact behavior of individual pages depend on available database content and assets.

### 2. Customer accounts

- Customer registration and login/logout routes.
- Integration with Django's built-in authentication system.
- Customer profile data associated with user records.
- Authenticated-user relationships for wishlists, reviews, and saved search history.

**Note:** Review account views and run authentication tests before using the site outside a local development environment.

### 3. Shopping cart and orders

- Add/remove quantity operations on order items.
- Order and order-item database models.
- Cart totals derived from item prices and quantities.
- Checkout and order-processing endpoints.
- Shipping-address model and transaction identifiers.
- Transaction-history view.

**Payment boundary:** The `process_order` code updates application order records. The repository does not establish a verified integration with a payment provider. Do not use this implementation to accept real payments without implementing and auditing proper payment verification.

### 4. Wishlists, ratings, and customer support

- Wishlist add/remove routes tied to user and product records.
- Review and rating models linked to products and users.
- Coupon model and discount-related logic.
- Contact form and support/help views.
- Return and exchange page routes.

Some page flows are represented by routes or model definitions but have not been independently verified end to end.

### 5. Community and interactive experiences

The repository also includes routes and data models for:

- Discussion topics and posts.
- Chat rooms and messages.
- Voice-chatbot interface.
- Geolocation-related pages.
- Camera, augmented-reality, virtual-room, virtual-try-on, and lipstick experiences.

These should be presented as experiments until their dependencies, permissions, and expected behavior have been demonstrated.

## Architecture

The platform is organized as a Django server-rendered web application:

```text
                 Browser / User Interface
                (HTML, CSS, JavaScript)
                           |
                           v
                   Django URL routing
                  ecom/ecom/urls.py
                           |
                           v
                    Store application
             views.py / forms.py / utils.py
                           |
             +-------------+-------------+
             |                           |
             v                           v
       Django models              Optional utilities
       (models.py)             (vision, geocoding,
             |                   recommendations)
             v
      SQLite database
      (local development)
```

**Request flow:** A browser requests a route, Django resolves it to a view, the view uses model or utility logic as needed, and a Django template or JSON response is returned. Shopping operations can update the relational database. Additional experimental utilities may require camera access or other services.

### Design decisions

| Concern | Current approach | Consideration |
| --- | --- | --- |
| Backend | Django and Python | Convenient authentication, ORM, routing, and templates |
| Persistence | SQLite | Appropriate for local development and demos |
| UI | Django templates, HTML, CSS, JavaScript | Server-rendered pages with interactive behaviors |
| Product media | Image fields and local static/media paths | Demo assets may be absent from the public repository |
| Recommendations | Search-history-related product matching | Simple baseline, not a validated AI recommender |
| Computer vision | OpenCV, MediaPipe, NumPy | Experimental; support varies by environment |
| Configuration | Environment variables for secrets | Keep credentials out of tracked source files |

## Technology stack

| Layer | Technology | Use |
| --- | --- | --- |
| Programming language | Python | Application logic and utilities |
| Web framework | Django | Models, routing, views, authentication, templates |
| Local database | SQLite | Product, customer, order, and related records |
| Frontend | HTML, CSS, JavaScript | Storefront and interactive views |
| Image processing | Pillow, OpenCV | Image handling and experimental visual features |
| Landmark / vision utilities | MediaPipe | Experimental camera/face functionality |
| Data and ML libraries | NumPy, pandas, scikit-learn | Supporting analytical/experimental modules |
| Geocoding | OpenCage | Optional geolocation integration |
| Version control | Git and GitHub | Source management and portfolio sharing |

`requirements.txt` lists package names without pinned versions. For reproducible deployment, the compatible dependency versions should eventually be locked and tested.

## Repository structure

```text
django-ecommerce/
Γö£ΓöÇΓöÇ README.md
Γö£ΓöÇΓöÇ .gitignore
ΓööΓöÇΓöÇ ecom/
    Γö£ΓöÇΓöÇ manage.py                 # Django management commands
    Γö£ΓöÇΓöÇ requirements.txt          # Python dependencies
    Γö£ΓöÇΓöÇ ecom/
    Γöé   Γö£ΓöÇΓöÇ settings.py           # Configuration and environment variables
    Γöé   Γö£ΓöÇΓöÇ urls.py               # Project-level URL routing
    Γöé   Γö£ΓöÇΓöÇ wsgi.py
    Γöé   ΓööΓöÇΓöÇ asgi.py
    Γö£ΓöÇΓöÇ store/
    Γöé   Γö£ΓöÇΓöÇ models.py             # Products, accounts, carts, orders, etc.
    Γöé   Γö£ΓöÇΓöÇ views.py              # Web and API endpoints
    Γöé   Γö£ΓöÇΓöÇ urls.py               # Store routes
    Γöé   Γö£ΓöÇΓöÇ forms.py              # Django forms
    Γöé   Γö£ΓöÇΓöÇ utils.py              # Shared shopping utilities
    Γöé   Γö£ΓöÇΓöÇ templates/store/      # Storefront templates
    Γöé   ΓööΓöÇΓöÇ ...                   # Additional utilities and modules
    Γö£ΓöÇΓöÇ chatbot/                  # Chatbot-related source
    Γö£ΓöÇΓöÇ chatbox/                  # Chat-related source
    Γö£ΓöÇΓöÇ static/                   # Locally available static resources
    ΓööΓöÇΓöÇ locale/                   # Localization resources
```

This is a simplified map rather than an exhaustive directory listing.

## Data model

The `store/models.py` file defines several interconnected entities:

| Model | Responsibility |
| --- | --- |
| `Category` | Groups products into catalogue categories |
| `Product` | Stores product attributes, image reference, pricing, and availability |
| `Customer` | Links customer details to a Django user |
| `Order` | Represents a customer's cart/order record |
| `OrderItem` | Associates products and quantities with an order |
| `ShippingAddress` | Stores an address linked to a customer/order |
| `WishlistItem` | Associates saved products with users |
| `ReviewRating` | Associates feedback and ratings with products/users |
| `Coupon` | Represents a time-bounded discount code |
| `SearchHistory` | Stores users' product-search terms |
| `ChatRoom`, `Message` | Support messaging-related experiments |
| `Topic`, `Post` | Support community discussion features |
| `VirtualTryOn` | Stores product-related try-on image records |
| `ProductAttribute` | Stores product variants such as color and size |
| `ContactMessage` | Captures contact form submissions |

**Data quality note:** The current `Product` model contains some repeated field declarations, and other parts of the code would benefit from refactoring. Avoid interpreting the present schema as a finalized production database design.

## Getting started

### Prerequisites

- Git
- Python 3 and `pip`
- A terminal (Windows PowerShell, macOS Terminal, or Linux shell)
- A modern browser

A local Django system check was completed during development using Python 3.14. This is **not** a guarantee that every experimental dependency works under Python 3.14 on all operating systems.

### 1. Clone the project

```bash
git clone https://github.com/ashimabhasin12/django-ecommerce.git
cd django-ecommerce
```

### 2. Set up a virtual environment

On Windows PowerShell:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, you can permit scripts for **only the current terminal process**:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

On macOS/Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

From the repository root:

```bash
python -m pip install -r ecom/requirements.txt
```

If an installation fails, check package compatibility with your Python version. The computer-vision packages can be more sensitive to platform and version differences than core Django.

### 4. Configure local secrets

`ecom/ecom/settings.py` reads `DJANGO_SECRET_KEY` from the environment and optionally reads `EMAIL_HOST_PASSWORD`. Do **not** paste real secrets into source code or commit `.env` files.

**Windows PowerShell:**

```powershell
$env:DJANGO_SECRET_KEY = python -c "import secrets; print(secrets.token_urlsafe(50))"
```

**macOS/Linux:**

```bash
export DJANGO_SECRET_KEY="$(python3 -c 'import secrets; print(secrets.token_urlsafe(50))')"
```

The generated key is available in that shell session. Generate and protect a different key for any future deployment.

SMTP/password-backed functionality is optional for local exploration; configure it only if needed, using a separately issued credential and an account/service you control.

### 5. Initialize your local database

```bash
cd ecom
python manage.py migrate
```

If you need the Django admin panel:

```bash
python manage.py createsuperuser
```

**Demo catalogue:** No complete seeded product database is guaranteed to be included. You may need to create categories and products through Django admin and provide your own licensed images.

### 6. Run the application

```bash
python manage.py check
python manage.py runserver
```

Open:

- Storefront: http://127.0.0.1:8000/
- Admin: http://127.0.0.1:8000/admin/

These are local development URLs. The project is **not configured for production hosting** in its current form.

### 7. Stop the development server

Press `Ctrl + C` in the terminal running `runserver`.

## Application routes

The current `store/urls.py` defines routes including:

| Path | Intended page or workflow |
| --- | --- |
| `/` | Main store |
| `/signup/`, `/login/`, `/logout/` | Account registration and sign-in/out |
| `/product-list/` | Product catalogue |
| `/product/<int:product_id>/` | Product detail route |
| `/shop/<slug:category_slug>/` | Category filtering |
| `/searchproduct/`, `/filter-products/` | Product discovery |
| `/cart/`, `/update_item/` | Cart and quantity updates |
| `/checkout/`, `/process_order/` | Checkout and order-record workflow |
| `/wishlist/` | Wishlist management |
| `/transaction-history/` | Order-related history |
| `/add_review/<int:product_id>/` | Customer reviews |
| `/return/`, `/exchange/` | Returns and exchanges pages |
| `/contact/`, `/help/` | Customer support |
| `/virtual-room/`, `/virtual-try-on/<int:product_id>/` | Experimental virtual experiences |
| `/lipstick/`, `/camera/`, `/ar/`, `/verify/` | Experimental vision routes |
| `/voice_chatbot/` | Voice-chatbot interface |
| `/admin/` | Django administration |

**Implementation note:** Some URL declarations and view signatures require review. A route appearing here does not guarantee that every click path works end to end.

## How the workflows fit together

### Product browsing

1. The customer visits the storefront.
2. A Django view retrieves product and category data from the database.
3. Django renders the storefront template.
4. The customer can navigate to product details, categories, or search results.

### Cart and order records

1. A customer selects a product and adjusts its quantity.
2. The application associates items with an order/cart record.
3. Cart totals are calculated from order items.
4. The checkout view displays the order summary and available checkout form.
5. An order-processing endpoint updates application-side order status.

**Important:** This is an application order workflow, not evidence that a payment processor has charged a customer. The implementation requires payment integration and security review before any real commercial use.

### Personalized product suggestions

For authenticated users, the storefront references saved search terms and queries products whose titles match those terms. This is a straightforward search-history recommendation baseline, **not** a demonstrated deep-learning recommender system.

## Experimental features

The codebase explores capabilities beyond standard e-commerce. These should be documented separately so reviewers can distinguish the core shopping architecture from experimental work.

### Virtual try-on and camera interfaces

Image and camera-related routes, virtual try-on data models, and computer-vision dependencies are present in the repository. Related experiences may depend on camera permission, specific image formats, and local assets. Recognition quality and real-time performance have not been independently benchmarked.

### Virtual lipstick / augmented reality

The repository includes lipstick and augmented-reality-related views. Their end-to-end status and device compatibility should be tested before demoing them as completed features.

### Voice chatbot and discussions

Routes and models for conversational and community functions are included. Any dependency on external services, microphone access, or additional environment settings should be documented when these modules are tested.

### Geolocation

The project lists OpenCage as a dependency and includes geolocation-related views. Any API-based integration needs a user-owned key and appropriate error handling. Never commit an API key.

## Configuration and security

This is a local development project. Before any internet-facing deployment, review at least the following:

- Set `DEBUG=False` and configure `ALLOWED_HOSTS` appropriately.
- Use unique environment-based secret keys and rotate any previously exposed credentials.
- Review CSRF handling and any endpoints decorated with `csrf_exempt`.
- Add authorization checks for account-owned orders, carts, and customer data.
- Validate all checkout amounts server-side; never trust a client-provided total as proof of payment.
- Set up production-safe static/media storage, HTTPS, secure cookies, and logging.
- Audit upload, camera, authentication, and email flows.
- Keep local databases, uploaded media, `.venv`, `.env`, and personal images out of Git.

**Known issue worth prioritizing:** The current source contains checkout-related endpoints using `csrf_exempt`; these should be reviewed before deployment.

## Testing

### Check Django configuration

From the `ecom/` directory:

```bash
python manage.py check
```

A local run of this command reported:

```text
System check identified no issues (0 silenced).
```

This only verifies Django's built-in system checks; it does not prove that every page, API, or purchase workflow functions correctly.

### Run automated tests

```bash
python manage.py test
```

The repository includes test-related files, but a passing complete test suite has **not** been established here. Save the test command output and exact dependency versions before declaring coverage or pass rates.

### Recommended manual test checklist

- [ ] Home page loads with a populated test catalogue.
- [ ] Product detail page displays correct information.
- [ ] Signup, login, and logout work.
- [ ] User can add/remove products and adjust cart quantity.
- [ ] Checkout displays correct totals and shipping details.
- [ ] Wishlist works for authenticated users.
- [ ] Reviews display and submit correctly.
- [ ] Search and category filtering return expected results.
- [ ] Unauthenticated users cannot access another user's private records.
- [ ] Experimental camera/voice pages handle unsupported devices gracefully.

Only mark a task complete after testing it.

## Troubleshooting

| Issue | What to check |
| --- | --- |
| `python` not found | Try `py --list` and `py --version` on Windows; check PATH and Python installation |
| PowerShell blocks activation | Use a process-scoped execution policy or call `.venv\Scripts\python.exe` directly |
| `KeyError: DJANGO_SECRET_KEY` | Set the environment variable in the terminal running Django |
| `No module named django` | Activate the correct virtual environment and install dependencies |
| Database tables missing | Run `python manage.py migrate` in the folder containing `manage.py` |
| Product pages are empty | Add demo categories/products and verify image paths |
| Media files not loading | Check media/static configuration and whether local files are available |
| Camera or vision features fail | Check camera permissions, supported package versions, and required local assets |
| Email functionality fails | Confirm host configuration and provide credentials privately via environment variables |

## Screenshots and demo


Suggested repository organization:

```text
docs/
ΓööΓöÇΓöÇ screenshots/
    Γö£ΓöÇΓöÇ storefront.png
    Γö£ΓöÇΓöÇ product-detail.png
    Γö£ΓöÇΓöÇ cart.png
    ΓööΓöÇΓöÇ virtual-try-on.png
```

## Acknowledgements and attribution

This repository is intended for learning, software engineering development, and portfolio presentation. Before presenting the project as solely authored, check the original course/team contributions and acknowledge collaborators where appropriate. The source currently contains at least one collaborator attribution in its comments. Also verify that all product images, templates, datasets, and third-party code are properly licensed for public distribution.

## Project link

**GitHub:** https://github.com/ashimabhasin12/django-ecommerce

---

*Built with Django and Python. The project is under development; functionality and security claims are limited to what has been tested.*

