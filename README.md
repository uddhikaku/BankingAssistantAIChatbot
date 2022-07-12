# BankingAssistantAIChatbot
AI to create unforgettable customer experiences.

Soul Machines is humanizing AI with hyper-realistic Digital People that adapt to real-time customer encounters while emulating appropriate emotions. They are always ready to assist customers, create engaging experiences, promote your brand, and develop meaningful connections.


<a href = "https://youtu.be/iCiXsfW_q14" ><img src="https://github.com/uddhikaku/BankingAssistantAIChatbot/blob/main/Banking%20Assistant%20Chatbot.png" width="50%" /></a>


#Code

---

#Main.py

import re
import long_responses as long


print()
print('Banking Assistant ChtBot')
print()

def message_probability(user_message, recognised_words, single_response=False, required_words=[]):
    message_certainty = 0
    has_required_words = True


    for word in user_message:
        if word in recognised_words:
            message_certainty += 1


    percentage = float(message_certainty) / float(len(recognised_words))


    for word in required_words:
        if word not in user_message:
            has_required_words = False
            break


    if has_required_words or single_response:
        return int(percentage * 100)
    else:
        return 0


def check_all_messages(message):
    highest_prob_list = {}


    def response(bot_response, list_of_words, single_response=False, required_words=[]):
        nonlocal highest_prob_list
        highest_prob_list[bot_response] = message_probability(message, list_of_words, single_response, required_words)

    # Responses -------------------------------------------------------------------------------------------------------
    response('Hello!', ['hello', 'hi', 'hey', 'sup', 'heyo'], single_response=True)
    response('See you!', ['bye', 'goodbye'], single_response=True)
    response('I\'m doing fine, and you?', ['how', 'are', 'you', 'doing'], required_words=['how'])
    response('You\'re welcome!', ['thank', 'thanks'], single_response=True)
    response('Thank you!', ['i', 'love', 'code', 'palace'], required_words=['code', 'palace'])
    response('Good Morning!', ['gm', 'morning'], single_response=True)
    response('Your Banking Assistant ChatBot is Here! How i can help you? ', ['banking', 'assistant'], required_words=['banking', 'assistant'])
    response('We Have Current Account, Savings Account, FD Account and etc, ', ['type', 'account'], required_words=['type', 'account'])

    # Longer responses
    response(long.R_ADVICE, ['give', 'advice'], required_words=['advice'])
    response(long.R_EATING, ['what', 'you', 'eat'], required_words=['you', 'eat'])

    best_match = max(highest_prob_list, key=highest_prob_list.get)


    return long.unknown() if highest_prob_list[best_match] < 1 else best_match



def get_response(user_input):
    split_message = re.split(r'\s+|[,;?!.-]\s*', user_input.lower())
    response = check_all_messages(split_message)
    return response



while True:

    print('Bot: ' + get_response(input('You: ')))



---

#long_responses.py

---

import re
import long_responses as long


print()
print('Banking Assistant ChtBot')
print()

def message_probability(user_message, recognised_words, single_response=False, required_words=[]):
    message_certainty = 0
    has_required_words = True


    for word in user_message:
        if word in recognised_words:
            message_certainty += 1


    percentage = float(message_certainty) / float(len(recognised_words))


    for word in required_words:
        if word not in user_message:
            has_required_words = False
            break


    if has_required_words or single_response:
        return int(percentage * 100)
    else:
        return 0


def check_all_messages(message):
    highest_prob_list = {}


    def response(bot_response, list_of_words, single_response=False, required_words=[]):
        nonlocal highest_prob_list
        highest_prob_list[bot_response] = message_probability(message, list_of_words, single_response, required_words)

    # Responses -------------------------------------------------------------------------------------------------------
    response('Hello!', ['hello', 'hi', 'hey', 'sup', 'heyo'], single_response=True)
    response('See you!', ['bye', 'goodbye'], single_response=True)
    response('I\'m doing fine, and you?', ['how', 'are', 'you', 'doing'], required_words=['how'])
    response('You\'re welcome!', ['thank', 'thanks'], single_response=True)
    response('Thank you!', ['i', 'love', 'code', 'palace'], required_words=['code', 'palace'])
    response('Good Morning!', ['gm', 'morning'], single_response=True)
    response('Your Banking Assistant ChatBot is Here! How i can help you? ', ['banking', 'assistant'], required_words=['banking', 'assistant'])
    response('We Have Current Account, Savings Account, FD Account and etc, ', ['type', 'account'], required_words=['type', 'account'])

    # Longer responses
    response(long.R_ADVICE, ['give', 'advice'], required_words=['advice'])
    response(long.R_EATING, ['what', 'you', 'eat'], required_words=['you', 'eat'])

    best_match = max(highest_prob_list, key=highest_prob_list.get)


    return long.unknown() if highest_prob_list[best_match] < 1 else best_match



def get_response(user_input):
    split_message = re.split(r'\s+|[,;?!.-]\s*', user_input.lower())
    response = check_all_messages(split_message)
    return response



while True:

    print('Bot: ' + get_response(input('You: ')))

