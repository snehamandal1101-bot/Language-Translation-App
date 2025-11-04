import ollama

def translate_text(text_to_translate: str, target_language: str, source_language: str = "auto"):
    
    prompt =("You are a language translator, Your only task is to accurately translate, your main goal is translate the text provided with the brief explanation.")

    
    user_query = (
        f"Translate the following text from {source_language} to {target_language}: "
        f"'{text_to_translate}'"
    )

    print(f"--- Translation Request ---")
    print(f"Source: {source_language} | Target: {target_language}")
    print(f"Text: '{text_to_translate}'\n")

    try:
        
        response = ollama.chat(
            model='gemma3:1b',
            messages=[
                {'role': 'system', 'content': prompt},                
                 {'role': 'user', 'content': user_query}
            ]
        )

        translated_text = response['message']['content'].strip()

        return translated_text

    
            
    
    except Exception as e:
        return f"An unexpected error occurred: {e}"



text_en = "Hello my name is Sneha Mandal."
translation_fr = translate_text(
    text_to_translate=text_en,
    source_language="English",
    target_language="Korea"
)
print("--- Result (Korea) ---")
print(f"'{translation_fr}'\n")

print("-" * 50)


