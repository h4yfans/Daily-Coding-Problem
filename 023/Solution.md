**Solution**

The idea here is to use either BFS or DFS to explore the board, starting from the start coordinate, and keep track of what we've seen so far as well as the steps from the start until we find the end coordinate.

In our case, we'll use BFS. We'll create a queue and initialize it with our start coordinate, along with a count of 0. We'll also initialize a `seen` set to ensure we only add coordinates we haven't seen before.

Then, as long as there's something still in the queue, we'll dequeue from the queue and first check if it's our target coordinate -- if it is, then we can just immediately return the count. Otherwise, we'll get the valid neighbours of the coordinate we're working with (valid means not off the board and not a wall), and enqueue them to the end of the queue.

To make sure the code doesn't get too messy, we'll define some helper functions: `walkable`, which returns whether or not a tile is valid, and `get_walkable_neighbours` which returns the valid neighbours of a coordinate.

    from collections import deque
    
    # Given a row and column, returns whether that tile is walkable.
    def walkable(board, row, col):
        if row < 0 or row >= len(board):
            return False
        if col < 0 or col >= len(board[0]):
            return False
        return not board[row][col]
    
    # Gets walkable neighbouring tiles.
    def get_walkable_neighbours(board, row, col):
        return [(r, c) for r, c in [
            (row, col - 1),
            (row - 1, col),
            (row + 1, col),
            (row, col + 1)]
            if walkable(board, r, c)
        ]
    
    def shortest_path(board, start, end):
        seen = set()
        queue = deque([(start, 0)])
        while queue:
            coords, count = queue.popleft()
            if coords == end:
                return count
            seen.add(coords)
            neighbours = get_walkable_neighbours(board, coords[0], coords[1])
            queue.extend((neighbour, count + 1) for neighbour in neighbours
                    if neighbour not in seen)
    
    board = [[False, False, False, False],
            [True, True, True, True],
            [False, False, False, False],
            [False, False, False, False]]
    
    print(shortest_path(board, (3, 0), (0, 0)))
    

This code should run in O(M \* N) time and space, since in the worst case we need to examine the entire board to find our target coordinate.
