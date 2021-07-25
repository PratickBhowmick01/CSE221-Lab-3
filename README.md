# CSE221-Lab-3
BFS &amp; DFS; Dictionary

#Task01
f = open("input1.txt", "r")
fp = open("output1.txt", "w")

vertex = int(f.readline()) 
edges = int(f.readline()) 

dict = {}
for i in range(0, edges):
    conn = f.readline()
    
    key, value = map(int,conn.split(" "))
    
    if (key not in dict): 
        dict[key] = list()
        list1 = [value]
        dict[key].extend(list1) 
        
    else:
        list2 = dict[key]        
        list2.append(value)
        dict[key] = list2
    
for x in dict:
    char = "Places: " + str(x) + " -> " + str(dict[x]) 
    fp.write(str(char))
    fp.write("\n")

fp.write("Victory Road reached!!")
f.close() 
fp.close() 


#Task02

f = open("input2.txt", "r")
fp = open("output2.txt", "w") 

from Task01 import dict  
from queue import Queue

visited = [0] * 12
graph = dict 
q = Queue(maxsize = 12)

def BFS(visited, graph, node, endPoint):
    visited[int(node)-1] = 1
    q.put(node) 

    fp.write("Places: ") 
    while(q.empty() != True):
        m = q.get() 
        fp.write(str(m)) 
        fp.write(" ")
        if (m == int(endPoint)): 
            break 
        
        if (int(m) in graph): 
            for i in graph[int(m)]:   
                if(visited[int(i) - 1] == 0):
                    visited[int(i)-1] = 1
                    q.put(i)

BFS(visited, graph, "1", "12") 

f.close() 
fp.close()


#Task03
f = open("input3.txt", "r")
fp = open("output3.txt", "w")
from Task01 import dict 

visited = [0]*12
printed = []    #this will store the graph traversing sequence
graph = dict

def DFS_VISIT(graph, node): 
    visited[node-1] = 1
    printed.append(str(node))   
    
    if (node in graph):  
        for j in graph[node]:
            if(visited[int(j)-1] == 0):
                DFS_VISIT(graph, j) 
            
def DFS(graph, endPoint):
    for i in graph:        
        if(visited[int(i)-1] == 0):
            DFS_VISIT(graph, i) 
    
    fp.write("Places: ")  
    for i in printed:
        fp.write(i) 
        fp.write(" ") 
        if(i == endPoint): 
            break        

DFS(graph, "12") 
f.close() 
fp.close() 




















