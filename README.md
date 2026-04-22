"""
Terracota Cafe - Streamlit App
Run with: streamlit run terracota_cafe.py
"""

import streamlit as st
from datetime import datetime, time

# ---------- PAGE CONFIG ----------
st.set_page_config(
    page_title="Terracota Cafe ☕",
    page_icon="☕",
    layout="wide",
    initial_sidebar_state="expanded",
)

# ---------- CUSTOM STYLES (terracotta theme) ----------
st.markdown(
    """
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;800&family=Inter:wght@400;600&display=swap');

        html, body, [class*="css"] { font-family: 'Inter', sans-serif; }

        .stApp {
            background: linear-gradient(180deg, #fdf6ee 0%, #f5e6d3 100%);
        }

        h1, h2, h3 {
            font-family: 'Playfair Display', serif !important;
            color: #4a2c1a !important;
        }

        /* Hero banner */
        .hero {
            background: linear-gradient(135deg, #c75d3a 0%, #e89060 100%);
            padding: 60px 40px;
            border-radius: 24px;
            color: white;
            box-shadow: 0 20px 50px -20px rgba(199, 93, 58, 0.5);
            margin-bottom: 30px;
        }
        .hero h1 { color: white !important; font-size: 3.2em; margin: 0; }
        .hero p { font-size: 1.2em; opacity: 0.95; margin-top: 10px; }

        /* Menu cards */
        .menu-card {
            background: white;
            padding: 20px 24px;
            border-radius: 16px;
            margin-bottom: 12px;
            box-shadow: 0 4px 15px rgba(74, 44, 26, 0.08);
            border-left: 4px solid #c75d3a;
            transition: transform 0.2s ease;
        }
        .menu-card:hover { transform: translateX(6px); }
        .menu-card h4 {
            color: #4a2c1a; margin: 0; font-family: 'Playfair Display', serif;
            display: flex; justify-content: space-between; align-items: center;
        }
        .price { color: #c75d3a; font-weight: 700; font-size: 1.1em; }
        .desc { color: #7a5a48; font-size: 0.92em; margin-top: 6px; }

        /* Sidebar */
        section[data-testid="stSidebar"] {
            background: linear-gradient(180deg, #4a2c1a 0%, #6b3f25 100%);
        }
        section[data-testid="stSidebar"] * { color: #fdf6ee !important; }

        /* Buttons */
        .stButton>button {
            background: linear-gradient(135deg, #c75d3a, #e89060);
            color: white; border: none; border-radius: 30px;
            padding: 10px 28px; font-weight: 600;
            box-shadow: 0 6px 20px -5px rgba(199, 93, 58, 0.5);
            transition: transform 0.2s;
        }
        .stButton>button:hover { transform: translateY(-2px); color: white; }

        /* Stat cards */
        .stat {
            background: white; padding: 24px; border-radius: 16px;
            text-align: center; box-shadow: 0 4px 15px rgba(74, 44, 26, 0.08);
        }
        .stat .num {
            font-family: 'Playfair Display', serif;
            font-size: 2.4em; color: #c75d3a; font-weight: 800;
        }
        .stat .lbl { color: #7a5a48; font-size: 0.85em; text-transform: uppercase; letter-spacing: 1px; }

        .footer {
            text-align: center; padding: 30px; color: #7a5a48;
            border-top: 1px solid #e0c9b0; margin-top: 40px;
        }
    </style>
    """,
    unsafe_allow_html=True,
)

# ---------- SIDEBAR NAVIGATION ----------
with st.sidebar:
    st.markdown("## ☕ Terracota Cafe")
    st.markdown("*A cosy place for coffee lovers*")
    st.markdown("---")
    choice = st.radio(
        "Navigate",
        ["🏠 Home", "🍽️ Menu", "📅 Reserve", "💬 About Us", "📞 Contact"],
        label_visibility="collapsed",
    )
    st.markdown("---")
    st.markdown("📍 **42 Clay Street**\nBandra West, Mumbai")
    st.markdown("🕗 Open daily · 8 AM – 11 PM")
    st.markdown("📞 +91 98765 43210")

# ---------- HOME ----------
if choice == "🏠 Home":
    st.markdown(
        """
        <div class="hero">
            <h1>Where every sip feels like home ☕</h1>
            <p>Artisan coffee · Honest food · Unhurried conversations</p>
        </div>
        """,
        unsafe_allow_html=True,
    )

    st.image(
        "https://images.unsplash.com/photo-1554118811-1e0d58224f24?w=1400",
        use_container_width=True,
    )

    st.markdown("### Why guests love us")
    c1, c2, c3, c4 = st.columns(4)
    stats = [("8+", "Years brewing"), ("50k", "Happy guests"),
             ("12", "Coffee origins"), ("100%", "Made fresh")]
    for col, (num, lbl) in zip([c1, c2, c3, c4], stats):
        col.markdown(f'<div class="stat"><div class="num">{num}</div><div class="lbl">{lbl}</div></div>',
                     unsafe_allow_html=True)

    st.markdown("### ")
    f1, f2, f3 = st.columns(3)
    f1.markdown("#### ☕ Artisan Brews\nSingle-origin beans, roasted weekly in-house.")
    f2.markdown("#### 🌱 Fresh & Local\nIngredients from neighbourhood farms.")
    f3.markdown("#### ❤️ Made with Love\nEvery plate, every cup — crafted with care.")

# ---------- MENU ----------
elif choice == "🍽️ Menu":
    st.markdown("# 🍽️ Our Menu")
    st.markdown("*Made fresh, served with love*")
    st.markdown("---")

    menu = {
        "☕ Coffee": [
            ("Espresso", "Bold double shot of single-origin Arabica.", 120),
            ("Cappuccino", "Velvety steamed milk, classic ratio. ⭐", 180),
            ("Caffè Latte", "Smooth espresso, silky textured milk.", 200),
            ("Flat White", "Microfoam, strong coffee character.", 210),
            ("Mocha", "Espresso, cocoa, steamed milk.", 220),
            ("Cold Brew", "Steeped 18 hours. Smooth, low-acid. 🏆", 230),
        ],
        "🥪 Bites & Mains": [
            ("Grilled Sandwich", "Sourdough, aged cheddar, garden tomato.", 150),
            ("Smash Burger", "House patty, caramelised onion, special sauce. ⭐", 220),
            ("Truffle Pasta", "Hand-rolled fettuccine, mushroom, parmesan.", 250),
            ("Pesto Wrap", "Basil pesto, grilled veg, sun-dried tomato.", 180),
        ],
        "🍰 Sweet Things": [
            ("Tiramisu", "Mascarpone, espresso-soaked ladyfingers.", 180),
            ("Banoffee Pie", "Caramel, banana, whipped cream.", 170),
            ("Chocolate Brownie", "Warm, gooey, served with ice cream.", 160),
        ],
        "🥤 Cold Drinks": [
            ("Iced Matcha", "Ceremonial-grade matcha, oat milk.", 240),
            ("Fresh Lemonade", "Hand-pressed lemon, mint, honey.", 140),
            ("Berry Smoothie", "Mixed berries, yoghurt, banana.", 200),
        ],
    }

    tabs = st.tabs(list(menu.keys()))
    for tab, (cat, items) in zip(tabs, menu.items()):
        with tab:
            for name, desc, price in items:
                st.markdown(
                    f"""
                    <div class="menu-card">
                        <h4>{name} <span class="price">₹{price}</span></h4>
                        <div class="desc">{desc}</div>
                    </div>
                    """,
                    unsafe_allow_html=True,
                )

# ---------- RESERVE ----------
elif choice == "📅 Reserve":
    st.markdown("# 📅 Reserve a Table")
    st.markdown("*We'd love to save you a seat*")
    st.markdown("---")

    col1, col2 = st.columns(2)
    with col1:
        name = st.text_input("Your Name")
        email = st.text_input("Email")
        phone = st.text_input("Phone")
    with col2:
        date = st.date_input("Date", min_value=datetime.today())
        slot = st.time_input("Time", value=time(19, 0))
        guests = st.number_input("Guests", min_value=1, max_value=12, value=2)

    notes = st.text_area("Special requests (optional)")

    if st.button("Confirm Reservation 🎉"):
        if name and email:
            st.success(
                f"✅ Booked! See you on **{date.strftime('%d %b %Y')}** at "
                f"**{slot.strftime('%I:%M %p')}** for **{guests}** guest(s), {name}."
            )
            st.balloons()
        else:
            st.error("Please fill in your name and email.")

# ---------- ABOUT ----------
elif choice == "💬 About Us":
    st.markdown("# 💬 Our Story")
    col1, col2 = st.columns([1, 1])
    with col1:
        st.image(
            "https://images.unsplash.com/photo-1511920170033-f8396924c348?w=800",
            use_container_width=True,
        )
    with col2:
        st.markdown(
            """
            ### A little cafe with a big heart

            Terracota started in **2017** — two friends, one small espresso machine,
            and a stubborn belief that a neighbourhood cafe could feel like a second home.

            Eight years later, the espresso machine is bigger, the menu is broader,
            but the soul is the same: warm walls, hanging plants, the hiss of steam,
            and conversations that meander from morning into evening.

            > *"We don't just serve coffee. We make space."*
            """
        )

    st.markdown("---")
    st.markdown("### What we stand for")
    v1, v2, v3, v4 = st.columns(4)
    v1.markdown("#### ❤️ Hospitality\nEvery guest is family.")
    v2.markdown("#### 🌱 Sustainable\nCompostable cups, local sourcing.")
    v3.markdown("#### 👥 Community\nLive music, book clubs, art shows.")
    v4.markdown("#### 🏆 Craft\nChampion baristas, trained chefs.")

# ---------- CONTACT ----------
elif choice == "📞 Contact":
    st.markdown("# 📞 Get in Touch")
    st.markdown("*Say hello — we'd love to hear from you*")
    st.markdown("---")

    col1, col2 = st.columns([1, 1])
    with col1:
        st.markdown("### Find us")
        st.markdown("📍 **Address**\n42 Clay Street, Bandra West, Mumbai 400050")
        st.markdown("📞 **Phone**\n+91 98765 43210")
        st.markdown("📧 **Email**\nhello@terracotacafe.in")
        st.markdown("🕗 **Hours**\nMon – Sun · 8:00 AM – 11:00 PM")
        st.map({"lat": [19.0596], "lon": [72.8295]}, zoom=14)

    with col2:
        st.markdown("### Send a message")
        c_name = st.text_input("Your Name", key="c_name")
        c_email = st.text_input("Your Email", key="c_email")
        c_subject = st.selectbox("Subject", ["General Inquiry", "Feedback", "Event Booking", "Partnership"])
        c_message = st.text_area("Your Message", height=140)
        if st.button("Send Message ✉️"):
            if c_name and c_email and c_message:
                st.success(f"Thanks {c_name}! Your message has been sent. 😊")
                st.snow()
            else:
                st.warning("Please fill in all fields.")

# ---------- FOOTER ----------
st.markdown(
    '<div class="footer">© 2025 Terracota Cafe · Made with ❤️ & espresso</div>',
    unsafe_allow_html=True,
)
