import streamlit as st
import openai

# Set your OpenAI API key here or via environment variable
openai.api_key = st.secrets["OPENAI_API_KEY"]

st.set_page_config(page_title="AI Blog Writing Agent", page_icon="🤖", layout="centered")

st.title("🤖 AI Blog Writing Agent")
st.write("Your AI partner for effortless, engaging blog writing.")

# Input section
topic = st.text_input("Enter your blog topic:")
keywords = st.text_area("Enter keywords (comma separated):")
tone = st.selectbox("Choose tone:", ["Professional", "Casual", "Storytelling", "Academic"])

if st.button("Generate Blog"):
    if topic:
        prompt = f"Write a {tone.lower()} blog post on '{topic}' including keywords: {keywords}. \
                  Make it engaging, structured with headings, and SEO-friendly."
        
        response = openai.Completion.create(
            engine="text-davinci-003",
            prompt=prompt,
            max_tokens=600,
            temperature=0.7
        )
        
        blog = response.choices[0].text.strip()
        st.subheader("Generated Blog Post:")
        st.write(blog)
    else:
        st.warning("Please enter a topic first.")
# 🤖 AI Blog Writing Agent

## Overview
This project is an AI-powered assistant that generates blog posts based on user input.  
It saves time, improves content quality, and provides SEO-friendly suggestions.

## Features
- Topic-based blog generation
- Keyword integration
- Tone & style customization
- SEO optimization tips

## How to Run
1. Clone this repo:
   ```bash
   git clone https://github.com/your-username/AI-Blog-Agent.git
   cd AI-Blog-Agent
