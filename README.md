import samino
import requests
import threading
sidd=os.environ["sid"]
email = "email"  # email
password = "password"  # password
chat = "http://aminoapps.com/p/7u1uf9"  # chat that you have host in it
community = "http://aminoapps.com/c/Btsarmy"  # community that you want to invite the online members of it

print("# Logging in")
client = samino.Client()
comId = client.get_from_link(community).comId
chat = client.get_from_link(chat)
try:
	client.login(email, password)
except:
	sid_login(sid=sidd)
	pass
#print(client.headers)

print("# Getting all online members")
local = samino.Local(comId)
curators = local.get_all_users("curators").userId
leaders = local.get_all_users("leaders").userId
leaders.extend(curators)
p
for i in range(0, 2100, 100):
    users = local.get_online_users(i, 100).userId
    if users: leaders.extend(users)
    else: break
def add_host(userId, comId, chatId, headers): print("#", requests.Session().post(f"https://service.narvii.com/api/v1/x{comId}/s/chat/thread/{chatId}/co-host/{userId}", headers=headers).json()["api:message"])

def remove_host(userId, comId, chatId, headers): print("#", requests.Session().delete(f"https://service.narvii.com/api/v1/x{comId}/s/chat/thread/{chatId}/co-host/{userId}", headers=headers).json()["api:message"])


print("# Starting\n")
for userId in leaders:
		try: threading.Thread(target=add_host,args=[userId, chat.comId, chat.objectId, client.headers]).start()
		except: pass
		try: threading.Thread(target=remove_host,args=[userId, chat.comId, chat.objectId, client.headers]).start()
		except: pass
