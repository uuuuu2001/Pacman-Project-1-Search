# Pacman-Project-1-Search

Question 1: DFS
#Dùng hàm problem.getStartState() để lấy vị trí ban đầu của Pacman
  start = problem.getStartState()
#Tạo stack để lưu các state
    stack = util.Stack()
    stack.push((start, []))
    visited = list()
#kiểm tra stack
    while not stack.isEmpty():
        #lấy ra phần tử đầu của ngăn xếp
        current, actions = stack.pop()
        #kiểm tra xem nếu đã đạt được đích thì trả về mảng các hành động
        if problem.isGoalState(current):
            return actions
        #nếu chưa thì thêm vào danh sách đã thăm qua
        if current not in visited:
            visited.append(current)
            #lấy state con của state hiện tại đưa vào stack
            successors = problem.getSuccessors(current)
            for state, action, cost in successors:
              #ghi lại các hành động và đưa vào stack
                newActions = actions + [action]
                stack.push((state, newActions))
    return []
  
  
Question 2: BFS  
#đẩy vị trí ban đầu vào queue được tạo nhằm lưu các vị trí
    start = problem.getStartState()
    queue = util.Queue()
    queue.push((start, []))
    visited = list()
    while not queue.isEmpty():
        current, actions = queue.pop()
        #kiểm tra xem nếu đã đạt được đích thì trả về mảng các hành động
        if problem.isGoalState(current):
            return actions
        #nếu chưa thì thêm vào danh sách đã thăm qua
        if current not in visited:
            visited.append (current)
            #lấy state con của state hiện tại đưa vào queue
            successors = problem.getSuccessors(current)
            #ghi lại các hành động
            for state, action, cost in successors:
                newActions = actions + [action]
                queue.push((state, newActions))
    return []

Question 3: uniformCostSearch
#sử dụng prority queue để lưu các vị trí
    start = problem.getStartState()
    priQueue = util.PriorityQueue()
    priQueue.update((start, []), 0)
    visited = list()
    
    #kiểm tra queue
    while not priQueue.isEmpty():
        current, actions = priQueue.pop()
        kiểm tra xem nếu đã đạt được đích thì trả về mảng các hành động
        if problem.isGoalState(current):
            return actions
        if current not in visited:
            visited.append(current)
            #lấy state con của state hiện tại đưa vào queue
            successors = problem.getSuccessors(current)
            #ghi lại
            for state, action, cost in successors:
                newActions = actions + [action]
                #ghi lại state tìm thấy với độ ưu tiên bằng tổng chi phí để đến state đó
                priQueue.update((state, newActions), problem.getCostOfActions(newActions))
    return []

Question 4: aStarSearch

    start = problem.getStartState()
    priQueue = util.PriorityQueue()
    priQueue.update((start, []), 0)
    visited = list()
    while not priQueue.isEmpty():
        current, actions = priQueue.pop()
        if problem.isGoalState(current):
            return actions
        if current not in visited:
            visited.append(current)
            successors = problem.getSuccessors(current)
            for state, action, cost in successors:
                newActions = actions + [action]
                #ghi lại state tìm thấy với độ ưu tiên bằng tổng chi phí + giá trị dự đoán
                priQueue.update((state, newActions), problem.getCostOfActions(newActions) + heuristic(state, problem))
    return []
