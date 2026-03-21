# Start a new tmux session
tmux new -s mysession

# Run your program
./your_program

# Detach with Ctrl+B, then D

# Later, reattach:
tmux attach -t mysession
