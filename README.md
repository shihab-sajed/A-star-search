# A-star-search
A * search algorithm python implementation
from queue import PriorityQueue

GRAPH = {
            'Natore': {'Sirajgonj': 135, 'Naogon': 70, 'Kushtia': 113},
            'Naogon': {'Natore': 70, 'Bogra': 66},
            'Bogra': {'Naogon': 66, 'Sirajgonj': 146},
            'Sirajgonj': {'Natore': 135, 'Bogra': 146, 'Mymenshing': 94, 'Tangail': 75},
            'Kushtia': {'Natore': 113, 'Rajbari': 106},
            'Rajbari': {'Kushtia': 106, 'Magura': 65},
            'Magura': {'Rajbari': 65, 'Faridpur': 70},
            'Faridpur': {'Magura': 70, 'Manikgonj': 115},
            'Manikgonj': {'Faridpur': 115, 'Tangail': 141, 'Gazipur': 133},
            'Tangail': {'Sirajgonj': 75, 'Manikgonj': 141, 'Gazipur': 92},
            'Mymenshing': {'Sirajgonj': 94, 'Dhaka': 206},
            'Gazipur': {'Tangail': 92, 'Manikgonj': 133, 'Dhaka': 96},
            'Dhaka': {'Mymenshing': 206, 'Gazipur': 96, 'Narayangonj': 90, 'Narshindi': 80},
            'Narayangonj': {'Dhaka': 90},
            'Narshindi': {'Dhaka': 80, 'Kishorgonj': 110},
            'Kishorgonj': {'Netrokona': 210, 'Narshindi': 110},
            'Netrokona': {'Kishorgonj': 210, 'Sunamgonj': 145},
            'Sunamgonj': {'Netrokona': 145}
        }



def a_star(source, destination):


    straight_line = {
                        'Natore': 361,
                        'Naogon': 369,
                        'Bogra': 375,
                        'Sirajgonj': 248,
                        'Kushtia': 324,
                        'Rajbari': 239,
                        'Magura': 236,
                        'Faridpur': 237,
                        'Manikgonj': 155,
                        'Tangail': 188,
                        'Mymenshing': 171,
                        'Gazipur': 95,
                        'Dhaka': 0,
                        'Narayangonj': 85,
                        'Narshindi': 105,
                        'Kishorgonj': 155,
                        'Netrokona': 204,
                        'Sunamgonj': 245
                    }

    p_q, visited = PriorityQueue(), {}
    p_q.put((straight_line[source], 0, source, [source]))
    visited[source] = straight_line[source]
    while not p_q.empty():
        (heuristic, cost, vertex, path) = p_q.get()
        print("Queue Status: ",heuristic, cost, vertex, path)
        if vertex == destination:
            return heuristic, cost, path
        for next_node in GRAPH[vertex].keys():
            current_cost = cost + GRAPH[vertex][next_node]
            heuristic = current_cost + straight_line[next_node]
            if not next_node in visited or visited[next_node] >= heuristic:
                visited[next_node] = heuristic
                p_q.put((heuristic, current_cost, next_node, path + [next_node]))

def main():

    print('Source :', end=' ')
    source = input().strip()
    print('Destination :', end=' ')
    goal = input().strip()
    if source not in GRAPH or goal not in GRAPH:
        print(' CITY DOES NOT EXIST.')
    else:
        heuristic, cost, optimal_path = a_star(source, goal)
        print('min of total heuristic_value =', heuristic)
        print('total min cost =', cost)
        print('\nRoute:')
        print(' -> '.join(city for city in optimal_path))


main()
#author shihab sajed


