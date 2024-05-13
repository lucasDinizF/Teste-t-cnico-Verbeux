import requests
import json

snapshot_version = '6640f4b899711ffb987053bc'
api_key = 'b18992f7-0fdb-11ef-b332-9679e3f28b2d'

link_firebase = "https://chatbot-64422-default-rtdb.firebaseio.com/"

headers = {
    'api-key': api_key
}

def get_new_chat():
    data = {
        'chatbot': 170,
        'snapshot_version': snapshot_version
    }
    response = requests.post('https://api.verbeux.com.br/dialog-manager-proxy/', json=data, headers=headers)


    if response.status_code != 200 or 'data' not in response.json():
        return None

    return response.json()['data']

def send_message(chat_id, message):
    data = {
        'message': message
    }
    response = requests.put(f"https://api.verbeux.com.br/dialog-manager-proxy/{chat_id}", json=data, headers=headers)


    if response.status_code != 200 or 'data' not in response.json():
        return ""

    return response.json()['data']['response'][0]['data'] or ""



if __name__ == "__main__":
    new_chat_data = get_new_chat()
    chat_id = new_chat_data['id']
    dataP = None
    dataN = None
    message2 = None
    message3 = None

    while True:
        message = input('User: ')
        response = send_message(chat_id, message)
        print(response)
        message2 = message


        if response == "Goodbye. Thank you for your message(s) of support.":
            break

        elif response == "Welcome, what would be your feedback?":
            message2 = None


        elif response == "Thanks for your feedback!! We always appreciate your support. Do you have any more feedback? If not, send a goodbye and end the conversation.":
            if message3 is not None or "positive" in message2 or "Positive" in message2:
                dataP = {'message': message3}
                requestPositive = requests.post(f'{link_firebase}/FeedbackPositive/.json', data=json.dumps(dataP))

            else:
                dataP = {'message': message2}
                requestPositive = requests.post(f'{link_firebase}/FeedbackPositive/.json', data=json.dumps(dataP))


        elif response == "Thanks for your feedback!! We will improve as much as possible. Do you have any more feedback? If not, send a goodbye and end the conversation.":
            if message3 is not None or "negative" in message2 or "Negative" in message2:
                dataN = {'message': message3}
                requestNegative = requests.post(f'{link_firebase}/FeedbackNegative/.json', data=json.dumps(dataN))

            else:
                dataN = {'message': message2}
                requestNegative = requests.post(f'{link_firebase}/FeedbackNegative/.json', data=json.dumps(dataN))

        elif response == "The following are negative feedbacks:":
            requestNegative = requests.get(f'{link_firebase}/FeedbackNegativo/.json')
            dictionary = requestNegative.json()
            print(dictionary)

        elif response == "Here are the positive feedbacks:":
            requestPositive = requests.get(f'{link_firebase}/FeedbackPositivo/.json')
            dictionary = requestPositive.json()
            print(dictionary)

        message3 = message2
