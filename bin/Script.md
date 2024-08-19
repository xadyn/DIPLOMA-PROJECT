import requests

# Замените 'YOUR_API_KEY' вашим фактическим API ключом
API_KEY = 'c6f262a299ec5d9295326c4dcb29bfe654648fe230b47adaf922da483687cfd7'
BASE_URL = 'https://www.virustotal.com/vtapi/v2'

def check_url(url):
    params = {
        'apikey': API_KEY,
        'url': url,
        'resource': url
    }
    
    # Отправляем запрос на проверку URL
    response = requests.get(f'{BASE_URL}/url/report', params=params)
    
    if response.status_code == 200:
        results = response.json()
        return results
    else:
        return None

def display_results(results):
    if results and 'positives' in results:
        print(f"URL: {results['url']}")
        print(f"Positive detections: {results['positives']} / {results['total']}")
        for scanner, result in results['scans'].items():
            print(f"{scanner}: {result['result']}")
    else:
        print("No results found or there was an error in the request.")

if __name__ == "__main__":
    url_to_check = input("Введите URL для проверки: ")
    results = check_url(url_to_check)
    display_results(results)