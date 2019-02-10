# Greedy 2 Algorithm for Set Cover Performed in Java                                  
完美啊，通过清晰地定义好各个lists之间的关系后，最后在main method中通过一个for loop简洁搞定了。
The class SolveSC is a list of lists. 

How to insert a 
```java
	public void SolveSC_insert (double w, int l, int subset_label) {
		Ground_List list = new Ground_List();
		list.label = subset_label;
		list.length = l;
		list.average_weight = w;
		list.active = false; // after adding all the elements of a subset to the list, list.active would switch to be true;
		if (ground_list == null) {
			ground_list = list;
		} else {
			Ground_List p=ground_list;
			while (p.next_set!=null) {
				if (p.average_weight>=list.average_weight) {
					list.next_set = p;
					if (p.previous_set != null) {
						list.previous_set = p.previous_set;
						p.previous_set.next_set = list;
					}
					p.previous_set = list;
					break;
				}
				p=p.next_set;
			}// if the while loop has not been broken, p.next_set == null currently;
			if (p.average_weight>=list.average_weight) {
				list.next_set = p;
				if (p.previous_set != null) {
					list.previous_set = p.previous_set;
					p.previous_set.next_set = list;
				}
				p.previous_set = list;
			} else if (p.average_weight<list.average_weight) {
				list.previous_set = p;
				p.next_set = list;
			}
		}
	}
```
                     
Best Regards!                              
Chuwei Zhou                
2019.2.9                  
