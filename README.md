# Ques 1.
    class SET:
        def __init__(self):
            self.elements = set()
    
        # Input elements
        def input_set(self):
            n = int(input("Enter number of elements: "))
            print("Enter elements:")
            for _ in range(n):
                self.elements.add(int(input()))
    
        # Display set
        def display(self):
            print(self.elements)
    
        # 1) ismember
        def ismember(self, x):
            return x in self.elements
    
        # 2) Power set
        def powerset(self):
            elems = list(self.elements)
            n = len(elems)
            print("Power Set:")
            for i in range(1 << n):
                subset = []
                for j in range(n):
                    if i & (1 << j):
                        subset.append(elems[j])
                print(set(subset))
    
        # 3) Subset
        def subset(self, other):
            return self.elements.issubset(other.elements)
    
        # 4) Union
        def union(self, other):
            result = SET()
            result.elements = self.elements.union(other.elements)
            return result
    
        # 4) Intersection
        def intersection(self, other):
            result = SET()
            result.elements = self.elements.intersection(other.elements)
            return result
    
        # 5) Complement
        def complement(self, universal):
            result = SET()
            result.elements = universal.elements - self.elements
            return result
    
        # 6) Difference
        def difference(self, other):
            result = SET()
            result.elements = self.elements - other.elements
            return result
    
        # 6) Symmetric Difference
        def symmetric_difference(self, other):
            result = SET()
            result.elements = self.elements.symmetric_difference(other.elements)
            return result
    
        # 7) Cartesian Product
        def cartesian_product(self, other):
            print("Cartesian Product:")
            for a in self.elements:
                for b in other.elements:
                    print((a, b), end=" ")
            print()


        # Menu-driven program
        A = SET()
        B = SET()
        U = SET()
        
        while True:
             print("\n----- MENU -----")
             print("1. Input Set A")
             print("2. Input Set B")
             print("3. Display Sets")
             print("4. Check Membership")
             print("5. Power Set")
             print("6. Subset Check (A ⊆ B)")
             print("7. Union")
             print("8. Intersection")
             print("9. Complement (A')")
             print("10. Difference (A - B)")
             print("11. Symmetric Difference")
             print("12. Cartesian Product")
             print("0. Exit")
    
    
        choice = int(input("Enter choice: "))
    
        if choice == 1:
            print("Set A:")
            A.input_set()
    
        elif choice == 2:
            print("Set B:")
            B.input_set()
    
        elif choice == 3:
            print("Set A =", A.elements)
            print("Set B =", B.elements)
    
        elif choice == 4:
            x = int(input("Enter element to check in A: "))
            print("Present" if A.ismember(x) else "Not Present")
    
        elif choice == 5:
            A.powerset()
    
        elif choice == 6:
            print("A is subset of B" if A.subset(B) else "A is NOT subset of B")
    
        elif choice == 7:
            result = A.union(B)
            print("Union =", result.elements)
    
        elif choice == 8:
            result = A.intersection(B)
            print("Intersection =", result.elements)
    
        elif choice == 9:
            print("Enter Universal Set:")
            U.input_set()
            result = A.complement(U)
            print("Complement of A =", result.elements)
    
        elif choice == 10:
            result = A.difference(B)
            print("A - B =", result.elements)
    
        elif choice == 11:
            result = A.symmetric_difference(B)
            print("Symmetric Difference =", result.elements)
    
        elif choice == 12:
            A.cartesian_product(B)
    
        elif choice == 0:
            print("Exiting...")
            break
    
        else:
            print("Invalid choice!")

# Ques 2.

    class RELATION:
        def __init__(self, n):
            self.n = n
             self.matrix = []

        def input_matrix(self):
            print("Enter relation matrix (0/1):")
            for i in range(self.n):
                row = list(map(int, input().split()))
                self.matrix.append(row)
    
        def display(self):
            print("Relation Matrix:")
            for row in self.matrix:
                print(row)
    
        def is_reflexive(self):
            for i in range(self.n):
                if self.matrix[i][i] != 1:
                    return False
            return True
    
        def is_symmetric(self):
            for i in range(self.n):
                for j in range(self.n):
                    if self.matrix[i][j] != self.matrix[j][i]:
                        return False
            return True
    
        def is_antisymmetric(self):
            for i in range(self.n):
                for j in range(self.n):
                    if i != j and self.matrix[i][j] == 1 and self.matrix[j][i] == 1:
                        return False
            return True
    
        def is_transitive(self):
            for i in range(self.n):
                for j in range(self.n):
                    if self.matrix[i][j] == 1:
                        for k in range(self.n):
                            if self.matrix[j][k] == 1 and self.matrix[i][k] != 1:
                                return False
            return True
    
        def check_relation(self):
            r = self.is_reflexive()
            s = self.is_symmetric()
            a = self.is_antisymmetric()
            t = self.is_transitive()
    
            print("\nProperties:")
            print("Reflexive:", r)
            print("Symmetric:", s)
            print("Anti-symmetric:", a)
            print("Transitive:", t)
    
            if r and s and t:
                print("Relation is an EQUIVALENCE RELATION")
            elif r and a and t:
                print("Relation is a PARTIAL ORDER RELATION")
    
            else:
                print("Relation is NONE")
    
        n = int(input("Enter number of elements: "))
        R = RELATION(n)
    
        R.input_matrix()
        R.display()
        R.check_relation()

# Ques 3.

    from itertools import permutations, product
    digits = input("Enter digits (space separated): ").split()
    r = int(input("Enter length of permutation: "))

    #1) Without Repetition
    print("\nPermutations WITHOUT repetition:")
    perm_without = permutations(digits, r)
    for p in perm_without:
        print(''.join(p), end=" ")
    print()

    #2) With Repetition
    print("\nPermutations WITH repetition:")
    perm_with = product(digits, repeat=r)
    for p in perm_with:
        print(''.join(p), end=" ")
    print()

# Ques 4.
    def find_solutions(n, C):
        solution = [0] * n

    def brute_force(index, remaining):
        if index == n - 1:
            solution[index] = remaining
            print(solution)
            return
      
        for i in range(remaining + 1):
            solution[index] = i
            brute_force(index + 1, remaining - i)

    brute_force(0, C)


    #Input
    n = int(input("Enter number of variables (n): "))
    C = int(input("Enter value of C (<=10): "))

    print("\nSolutions:")
    find_solutions(n, C)

# Ques 5.
    degree = int(input("Enter degree of polynomial: "))

    #Example: for 4x^2 + 2x + 9 → enter: 4 2 9
    coeff = list(map(int, input("Enter coefficients: ").split()))

    x = int(input("Enter value of x: "))

    #Evaluate polynomial
    result = 0
    for i in range(degree + 1):
        result += coeff[i] * (x ** (degree - i))

    print("Value of polynomial =", result)

# Ques 6.
    class Graph:
        def __init__(self, n):
            self.n = n
            self.matrix = []

    def input_matrix(self):
        print("Enter adjacency matrix:")
        for i in range(self.n):
            row = list(map(int, input().split()))
            self.matrix.append(row)

    def is_complete(self):
        for i in range(self.n):
            for j in range(self.n):
                if i == j:
                    if self.matrix[i][j] != 0:
                        return False
                else:
                    if self.matrix[i][j] != 1:
                        return False
        return True

    def display(self):
        print("Adjacency Matrix:")
        for row in self.matrix:
            print(row)


    #Main program
    n = int(input("Enter number of vertices: "))
    g = Graph(n)

    g.input_matrix()
    g.display()

    if g.is_complete():
        print("Graph is a COMPLETE GRAPH")
    else:
        print("Graph is NOT a complete graph")

# Ques 7.
    class Graph:
        def __init__(self, n):
            self.n = n
            self.adj_list = {i: [] for i in range(n)}

    def input_graph(self):
        print("Enter adjacency list (space separated neighbors):")
        for i in range(self.n):
            self.adj_list[i] = list(map(int, input(f"Neighbors of {i}: ").split()))

    def is_complete(self):
        for vertex in self.adj_list:
            neighbors = set(self.adj_list[vertex])
            if vertex in neighbors:
                neighbors.remove(vertex)

            if len(neighbors) != self.n - 1:
                return False

            for v in range(self.n):
                if v != vertex and v not in neighbors:
                    return False

        return True

    def display(self):
        print("Adjacency List:")
        for v in self.adj_list:
            print(v, "->", self.adj_list[v])


    #Main program
    n = int(input("Enter number of vertices: "))
    g = Graph(n)

    g.input_graph()
    g.display()

    if g.is_complete():
        print("Graph is a COMPLETE GRAPH")
    else:
        print("Graph is NOT a complete graph")

# Ques 8.
    class Graph:
        def __init__(self, n):
            self.n = n
            self.matrix = []

        def input_matrix(self):
            print("Enter adjacency matrix (0/1):")
            for i in range(self.n):
                row = list(map(int, input().split()))
                self.matrix.append(row)
    
        def compute_degrees(self):
            print("\nVertex\tIn-Degree\tOut-Degree")
            
            for i in range(self.n):
                out_degree = sum(self.matrix[i])  # row sum
                in_degree = sum(self.matrix[j][i] for j in range(self.n))  # column sum
            
                print(f"{i}\t{in_degree}\t\t{out_degree}")


    #Main program
    n = int(input("Enter number of vertices: "))
    g = Graph(n)
    
    g.input_matrix()
    g.compute_degrees()





