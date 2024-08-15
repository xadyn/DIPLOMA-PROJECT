1)Установленый на Ubuntu 20.04 Setoolkit
![SET](https://github.com/user-attachments/assets/b015e803-81bd-46cd-a630-2e7ad26ed207)
1.1)Отрабатывает штатно (если требуется смогу развернуть минут 15
![Setoolkit](https://github.com/user-attachments/assets/fcde9ba6-c2ab-4336-aa8e-9d6ae9453977)

2)Можно немного скрипта на пайтоне добавить 
python
import requests

API_KEY = 'c6f262a299ec5d9295326c4dcb29bfe654648fe230b47adaf922da483687cfd7'
BASE_URL = 'https://www.virustotal.com/vtapi/v2'

def check_url(url):
    params = {
        'apikey': API_KEY,
        'url': url }
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
        print("Нет результата")
if __name__ == "__main__":
    url_to_check = input("Введите URL для проверки: ")
    results = check_url(url_to_check)
    display_results(results)
