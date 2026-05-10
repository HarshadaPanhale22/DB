1. Implement depth first search algorithm and Breadth First Search algorithm, Use an undirected graph and develop a recursive algorithm for searching all thevertices of a graph or tree data structure.
   

from collections import deque                             
from collections import deque

class Graph:

    def __init__(self):
        self.graph = {}

    # Add edge
    def add_edge(self, u, v):

        if u not in self.graph:
            self.graph[u] = []

        if v not in self.graph:
            self.graph[v] = []

        self.graph[u].append(v)
        self.graph[v].append(u)

    # DFS
    def dfs(self, start, visited=None):

        if visited is None:
            visited = set()

        print(start, end=" ")
        visited.add(start)

        for neighbor in self.graph[start]:

            if neighbor not in visited:
                self.dfs(neighbor, visited)

    # BFS
    def bfs(self, start):

        visited = set()
        queue = deque([start])

        visited.add(start)

        while queue:

            node = queue.popleft()

            print(node, end=" ")

            for neighbor in self.graph[node]:

                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append(neighbor)


# Create graph
g = Graph()

g.add_edge(0, 1)
g.add_edge(0, 2)
g.add_edge(1, 3)
g.add_edge(1, 4)
g.add_edge(2, 5)
g.add_edge(2, 6)

# DFS
print("DFS Traversal:")
g.dfs(0)

# BFS
print("\n\nBFS Traversal:")
g.bfs(0)
--------------------------------------------------------------------------------------------------------------------------
2.Implement A star Algorithm for any game search problem.
import heapq

import heapq

# Maze
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

    pq = []
    heapq.heappush(pq, (0, start))

    visited = set()
    parent = {}

    while pq:

        cost, current = heapq.heappop(pq)

        # Goal found
        if current == goal:

            path = []

            while current in parent:
                path.append(current)
                current = parent[current]

            path.append(start)
            path.reverse()

            return path

        visited.add(current)

        # Directions
        moves = [(0,1), (1,0), (0,-1), (-1,0)]

        for move in moves:

            row = current[0] + move[0]
            col = current[1] + move[1]

            next_node = (row, col)

            # Check valid path
            if (0 <= row < 4 and
                0 <= col < 4 and
                maze[row][col] == 0 and
                next_node not in visited):

                priority = heuristic(next_node, goal)

                heapq.heappush(pq, (priority, next_node))

                parent[next_node] = current

    return None


# Run
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

        # Greetings
        greetings = [
            "Hello! How can I help you?",
            "Hi there!",
            "Welcome!"
        ]

        # Responses
        product_info = "We sell laptops and mobiles."

        pricing_info = "Prices start from ₹10,000."

        order_info = "Please provide your order ID."

        complaint_response = "Sorry for the issue. Please explain your problem."

        goodbyes = [
            "Thank you! Goodbye!",
            "Have a nice day!",
            "Visit again!"
        ]

        # Check message
        if any(word in message for word in ["hello", "hi", "hey"]):
            return random.choice(greetings)

        elif any(word in message for word in ["product", "item"]):
            return product_info

        elif any(word in message for word in ["price", "cost"]):
            return pricing_info

        elif any(word in message for word in ["order", "track"]):
            return order_info

        elif any(word in message for word in ["complaint", "problem"]):
            return complaint_response

        elif any(word in message for word in ["bye", "goodbye"]):
            return random.choice(goodbyes)

        else:
            return "Sorry, I did not understand."


# Create chatbot
chatbot = CustomerChatbot("Customer Support Bot")

print("=== Welcome to Customer Support ===")

while True:

    user_input = input("You: ")

    response = chatbot.respond(user_input)

    print(chatbot.name + ":", response)

    if "bye" in user_input.lower():
        break
-----------------------------------------------------------------------------------------------------

6.Implement any one of the following Expert System Information management

    # Empty book list
books = []

while True:

    print("\n=== Library Management System ===")
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

        print("Book Added Successfully")

    # View Books
    elif choice == "2":

        if len(books) == 0:
            print("No Books Available")

        else:
            for book in books:

                print("\nBook Details")
                print("ID:", book["id"])
                print("Title:", book["title"])
                print("Author:", book["author"])
                print("Year:", book["year"])

    # Search Book
    elif choice == "3":

        search = input("Enter Book Title: ")

        found = False

        for book in books:

            if search.lower() == book["title"].lower():

                print("\nBook Found")
                print(book)

                found = True

        if not found:
            print("Book Not Found")

    # Delete Book
    elif choice == "4":

        delete_id = input("Enter Book ID to Delete: ")

        found = False

        for book in books:

            if delete_id == book["id"]:

                books.remove(book)

                print("Book Deleted Successfully")

                found = True
                break

        if not found:
            print("Book Not Found")

    # Exit
    elif choice == "5":

        print("Thank You")
        break

    else:
        print("Invalid Choice")
