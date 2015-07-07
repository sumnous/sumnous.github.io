```
Algorithm: 
———————————————————————
Input：Bipartite Network G （user-topic）
Initial：initial topic_label and user_label is None
T = 40
flag = True
Q_ov_dict = {}
while True: 
	if flag == True:
		user_label = update_user_label(user_label, topic_label)
		communities = get_community_result(user_label, topic_label)
		Q_ov = get_modularity(communities)
		Q_ov_dict[Q_ov] = communities
	else:
		topic_label = update_topic_label(user_label, topic_label)
	if T == 0:
		break
	else:
		T -= 1
		flag = not flag
Q_ov_max = max(Q_ov_dict.keys())
Output: [Q_ov_max, Q_ov_dict[Q_ov_max]]
```
