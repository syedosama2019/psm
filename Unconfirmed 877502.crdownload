import streamlit as st
import re  # Import for regular expressions

def evaluate_password(password):
    """
    Function to evaluate password strength and provide feedback.
    """
    score = 0  # Initialize password strength score
    feedback = []  # Store improvement suggestions

    # 1. Check password length (Minimum 8 characters)
    if len(password) >= 8:
        score += 1
    else:
        feedback.append("🔹 Make your password at least 8 characters long.")

    # 2. Check for uppercase letters
    if re.search(r'[A-Z]', password):
        score += 1
    else:
        feedback.append("🔹 Include at least one uppercase letter.")

    # 3. Check for lowercase letters
    if re.search(r'[a-z]', password):
        score += 1
    else:
        feedback.append("🔹 Include at least one lowercase letter.")

    # 4. Check for digits (0-9)
    if re.search(r'\d', password):
        score += 1
    else:
        feedback.append("🔹 Include at least one digit (0-9).")

    # 5. Check for special characters (!@#$%^&*)
    if re.search(r'[!@#$%^&*]', password):
        score += 1
    else:
        feedback.append("🔹 Include at least one special character (!@#$%^&*).")

    # Determine password strength based on the score
    if score == 5:
        strength = "✅ Strong Password! Your password meets all security requirements."
        color = "green"
    elif 3 <= score <= 4:
        strength = "⚠️ Moderate Password. Consider making it stronger."
        color = "orange"
    else:
        strength = "❌ Weak Password. You should improve your password using the suggestions below."
        color = "red"

    return score, strength, feedback, color


# ---- Streamlit UI ----
st.set_page_config(page_title="Password Strength Meter", page_icon="🔒", layout="centered")

st.title("🔒 Password Strength Meter")
st.write("Enter your password below to check its strength and get suggestions for improvement.")

# User input (Password field)
password = st.text_input("Enter Password:", type="password")

# Initialize variables to avoid NameError
strength_message = ""
color = "black"
feedback = []
score = 0

if password:  # Ensure password is not empty
    score, strength_message, feedback, color = evaluate_password(password)

    # Display strength message
    st.markdown(f"**Password Strength:** <span style='color:{color}; font-weight:bold'>{strength_message}</span>", unsafe_allow_html=True)

    # Progress bar based on score
    st.progress(score / 5)

    # Show suggestions if password is not strong
    if feedback:
        st.subheader("Suggestions to improve your password:")
        for tip in feedback:
            st.write(f"- {tip}")

# Footer
st.markdown("<br><hr><center>🔐 Built with Streamlit</center>", unsafe_allow_html=True)
