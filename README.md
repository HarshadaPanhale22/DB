1. Implement depth first search algorithm and Breadth First Search algorithm, Use an undirected graph and develop a recursive algorithm for searching all thevertices of a graph or tree data structure.
   

from collections import deque                             

class Graph:
    def __init__(self):
        # Adjacency list representation
        self.graph = {}

    # Add an undirected edge
    def add_edge(self, u, v):
        if u not in self.graph:
            self.graph[u] = []
        if v not in self.graph:
            self.graph[v] = []

        self.graph[u].append(v)
        self.graph[v].append(u)

    # Depth First Search (DFS)
    def dfs(self, start, visited=None):
        if visited is None:
            visited = set()

        print(start, end=" ")
        visited.add(start)

        for neighbor in self.graph[start]:
            if neighbor not in visited:
                self.dfs(neighbor, visited)

    # Breadth First Search (BFS)
    def bfs(self, start):
        visited = set()
        queue = deque([start])

        visited.add(start)
        while queue:
            vertex = queue.popleft()
            print(vertex, end=" ")

            for neighbor in self.graph[vertex]:
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append(neighbor)
#example
g = Graph()

g.add_edge(0, 1)
g.add_edge(0, 2)
g.add_edge(1, 3)
g.add_edge(1, 4)
g.add_edge(2, 5)
g.add_edge(2, 6)
g.add_edge(3,7)
g.add_edge(3,8)
g.add_edge(4,9)
print("DFS Traversal:")
g.dfs(0)

print("\n\nBFS Traversal:")
g.bfs(0)

--------------------------------------------------------------------------------------------------------------------------
2.Implement A star Algorithm for any game search problem.
import heapq

# Maze (0 = open path, 1 = wall)
maze = [
    [0, 0, 0, 0],
    [1, 1, 0, 1],
    [0, 0, 0, 1],
    [0, 1, 0, 0]
]

start = (0, 0)
goal = (3, 3)

# Heuristic Function
def heuristic(a, b):
    return abs(a[0] - b[0]) + abs(a[1] - b[1])

# A* Algorithm
def a_star(maze, start, goal):

    rows = len(maze)
    cols = len(maze[0])

    pq = []   # Priority Queue
    heapq.heappush(pq, (0, start))

    visited = set()
    parent = {}

    while pq:

        cost, current = heapq.heappop(pq)

        # Goal reached
        if current == goal:

            path = []

            while current in parent:
                path.append(current)
                current = parent[current]

            path.append(start)
            path.reverse()

            return path

        visited.add(current)

        # Move directions
        directions = [(0,1), (1,0), (0,-1), (-1,0)]

        for d in directions:

            new_row = current[0] + d[0]
            new_col = current[1] + d[1]

            next_node = (new_row, new_col)

            # Check valid position
            if (0 <= new_row < rows and
                0 <= new_col < cols and
                maze[new_row][new_col] == 0 and
                next_node not in visited):

                priority = heuristic(next_node, goal)

                heapq.heappush(pq, (priority, next_node))

                parent[next_node] = current

    return None

# Run Algorithm
path = a_star(maze, start, goal)

if path:
    print("Path Found:", path)
else:
    print("No Path Found")

--------------------------------------------------------------------------------------------------------------

3.Greedy search algorithm for any of the following application Minimum Spanning Tree
import heapq

class Graph:
    def __init__(self, vertices):
        self.v = vertices
        self.graph = [[] for _ in range(vertices)]

    def add_edge(self, u, v, w):
        # Add edge in both directions
        self.graph[u].append((w, v))
        self.graph[v].append((w, u))

    def prim_mst(self):
        visited = [False] * self.v
        pq = [(0, 0)]   # (weight, vertex)
        total_cost = 0

        while pq:
            weight, u = heapq.heappop(pq)

            if visited[u]:
                continue

            visited[u] = True
            total_cost += weight

            for w, v in self.graph[u]:
                if not visited[v]:
                    heapq.heappush(pq, (w, v))

        return total_cost


# Example
g = Graph(4)

g.add_edge(0, 1, 1)
g.add_edge(0, 2, 4)
g.add_edge(1, 2, 2)
g.add_edge(1, 3, 5)
g.add_edge(2, 3, 3)


print("Total cost of Minimum Spanning Tree:", g.prim_mst())
-----------------------------------------------------------------------------------------------------------------

4. Implement a solution for a Constraint Satisfaction Problem using Branch and Bound and Backtracking for n-queens problem or a graph coloring problem.

# Size of chess board
N = 5

# Empty board
board = [[0 for i in range(N)] for j in range(N)]

# Check if queen can be placed
def is_safe(row, col):

    # Check column
    for i in range(row):
        if board[i][col] == 1:
            return False

    # Check left diagonal
    i = row - 1
    j = col - 1

    while i >= 0 and j >= 0:
        if board[i][j] == 1:
            return False
        i -= 1
        j -= 1

    # Check right diagonal
    i = row - 1
    j = col + 1

    while i >= 0 and j < N:
        if board[i][j] == 1:
            return False
        i -= 1
        j += 1

    return True


# Solve N-Queen problem
def solve(row):

    # All queens placed
    if row == N:
        return True

    for col in range(N):

        if is_safe(row, col):

            # Place queen
            board[row][col] = 1

            # Place next queen
            if solve(row + 1):
                return True

            # Backtrack
            board[row][col] = 0

    return False


# Run program
solve(0)

# Print board
for i in range(N):
    for j in range(N):

        if board[i][j] == 1:
            print("Q", end=" ")
        else:
            print(".", end=" ")

    print()
-------------------------------------------------------------------------------------------------------------------------------------

5. Develop an elementary catboat for any suitable customer interaction application.

    import random 
class CustomerChatbot: 
def __init__(self, name): 
self.name = name 
def respond(self, message): 
message = message.lower()      
# Greeting responses 
greetings = ["Hello! How can I assist you today?", 
"Hi there! What can I help you with?", 
"Welcome! How may I help you?"] 
# Product information 
product_info = "We offer laptops, smartphones, and accessories. Which product would you 
like information about?" 
# Pricing information 
pricing_info = "Our prices start from ₹10,000. Please specify the product for exact pricing. 
# Order tracking 
order_info = "Please provide your order ID to track your order. 
# Complaint response 
complaint_response = "I'm sorry for the inconvenience. Please describe your issue in detail 
so I can assist you.  
# Goodbye responses 
goodbyes = ["Thank you for visiting! Have a great day!", 
"Goodbye! Feel free to contact us again.", 
"Take care! We are always here to help."] 
# Intent detection using keywords 
if any(word in message for word in ["hello", "hi", "hey"]): 
return random.choice(greetings) 
elif any(word in message for word in ["product", "item", "service"]): 
return product_info 
elif any(word in message for word in ["price", "cost", "rate"]): 
return pricing_info 
elif any(word in message for word in ["order", "track", "delivery"]): 
return order_info 
elif any(word in message for word in ["complaint", "problem", "issue"]): 
return complaint_response 
elif any(word in message for word in ["bye", "goodbye", "thank you"]): 
return random.choice(goodbyes) 
else: 
return "I'm sorry, I didn't understand your request. Could you please rephrase? 
# Create chatbot instance 
chatbot = CustomerChatbot("Customer Support Bot" 
print("---- Welcome to Customer Support ----") 
while True: 
user_input = input("You: ") 
response = chatbot.respond(user_input) 
print(chatbot.name + ": " + response) 
if any(word in user_input.lower() for word in ["bye", "goodbye"]): 
break

-----------------------------------------------------------------------------------------------------

6.Implement any one of the following Expert System Information management

      books = [] 
while True: 
print("\nLibrary Management System") 
print("1. Add Book") 
print("2. View Books") 
print("3. Search Book") 
print("4. Delete Book") 
print("5. Exit") 
choice = input("Enter your choice: ") 
# Add Book 
if choice == "1": 
book_id = input("Enter Book ID: ") 
title = input("Enter Book Title: ") 
author = input("Enter Author Name: ") 
year = input("Enter Year: ") 
book = { 
"id": book_id, 
"title": title, 
"author": author, 
"year": year 
} 
books.append(book) 
print("Book added successfully.") 
# View Books 
elif choice == "2": 
if len(books) == 0: 
print("No books available.") 
else: 
for book in books: 
print("ID:", book["id"]) 
print("Title:", book["title"]) 
print("Author:", book["author"]) 
print("Year:", book["year"]) 
print("-------------------") 
# Search Book 
elif choice == "3": 
search = input("Enter title to search: ") 
found = False 
for book in books: 
if search.lower() == book["title"].lower(): 
print("Book Found:") 
print(book) 
found = True 
if not found: 
print("Book not found.") 
# Delete Book 
elif choice == "4": 
delete_id = input("Enter Book ID to delete: ") 
found = False 
for book in books: 
if delete_id == book["id"]: 
books.remove(book) 
print("Book deleted successfully.") 
found = True 
break 
if not found: 
print("Book not found.") 
# Exit 
elif choice == "5": 
print("Thank you!") 
break 
else: 
print("Invalid choice.")
