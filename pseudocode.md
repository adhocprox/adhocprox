# get initial neighbors and order them based on ID
loop 5 seconds:
    known_nodes = discovery()
    known_nodes = sort(known_nodes)

# the device with the smallest ID starts the round robin process
if me == known_nodes[0]:
    my_turn = true

loop:
    # ranging packets include a flag to indicate whose turn it is
    my_turn = respond_to_ranging()
    
    if my_turn:
        # do discovery to find new neighbors
        known_nodes = discovery()
        known_nodes = sort(known_nodes)

        # range to every other node
        for node in known_nodes:
            if node != me:
                do_ranging(node)
        signal_next_node_to_range()
