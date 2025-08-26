import streamlit as st
import requests
import os
from pytube import YouTube
from youtube_search import YoutubeSearch

# -----------------------------
# Function: YouTube search
# -----------------------------
def search_youtube(query):
    results = YoutubeSearch(query, max_results=5).to_dict()
    return results

# -----------------------------
# Function: Check if video exists
# -----------------------------
def check_video_on_youtube(video_link):
    try:
        # اگر یہ یوٹیوب لنک ہے تو direct چیک کرو
        if "youtube.com" in video_link or "youtu.be" in video_link:
            try:
                yt = YouTube(video_link)
                return f"✅ یہ ویڈیو پہلے سے YouTube پر موجود ہے: {yt.title}"
            except:
                return "❌ یہ لنک یوٹیوب پر valid نہیں ہے۔"
        
        # اگر یوٹیوب نہیں ہے (فیس بک، ٹک ٹاک وغیرہ)
        else:
            # Title/Description match کرنے کی کوشش
            query = video_link.split("/")[-1]  # simple fallback
            results = search_youtube(query)
            if results:
                return f"⚠️ ممکن ہے یہ ویڈیو YouTube پر پہلے سے موجود ہو: {results[0]['title']}"
            else:
                return "❌ یہ ویڈیو YouTube پر نہیں ملی۔"
    except Exception as e:
        return f"⚠️ Error: {str(e)}"


# -----------------------------
# Streamlit App
# -----------------------------
st.title("🔎 YouTube Video Duplicate Checker")
st.write("Paste any video link (Facebook, TikTok, etc.) and check if it's already uploaded on YouTube.")

video_link = st.text_input("🎥 Video Link:")

if st.button("Check Now"):
    if video_link:
        result = check_video_on_youtube(video_link)
        st.success(result)
    else:
        st.warning("⚠️ Please enter a video link first.")
