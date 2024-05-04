class DistanceVectorRouter:
    def __init__(self, router_id, neighbors):
        self.router_id = router_id
        self.neighbors = neighbors
        self.routing_table = {neighbor: {'cost': neighbors[neighbor], 'next_hop': neighbor} for neighbor in neighbors}
        self.routing_table[self.router_id] = {'cost': 0, 'next_hop': self.router_id}

    def update_routing_table(self, neighbor, costs):
        for dest, cost in costs.items():
            total_cost = cost + self.routing_table[neighbor]['cost']
            if dest not in self.routing_table or total_cost < self.routing_table[dest]['cost']:
                self.routing_table[dest] = {'cost': total_cost, 'next_hop': neighbor}

    def send_routing_table(self):
        return self.router_id, self.routing_table

    def receive_routing_table(self, neighbor_id, neighbor_table):
        self.update_routing_table(neighbor_id, neighbor_table)

    def print_routing_table(self):
        print(f"Routing table for Router {self.router_id}:")
        for dest, info in self.routing_table.items():
            print(f"Destination: {dest}, Cost: {info['cost']}, Next Hop: {info['next_hop']}")


# Example network topology
network = {
    'A': {'B': 1, 'C': 5},
    'B': {'A': 1, 'C': 3},
    'C': {'A': 5, 'B': 3}
}

routers = {}
for router_id, neighbors in network.items():
    routers[router_id] = DistanceVectorRouter(router_id, neighbors)

# Simulation
for _ in range(3):  # Number of iterations
    for router_id, router in routers.items():
        for neighbor_id in router.neighbors:
            neighbor_router = routers[neighbor_id]
            neighbor_table = {router_id: router.neighbors[neighbor_id]}
            neighbor_router.receive_routing_table(router_id, neighbor_table)

# Output routing tables
for router_id, router in routers.items():
    router.print_routing_table()
