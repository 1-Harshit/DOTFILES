# bad but ok
alias ll="ls -alrth"
alias jj="jobs -l"
alias c="clear"
alias qq="exit"
alias rsynch="rsync -vPtrlz"


# loop function
function _loop () {
	local flist=$1
	shift 1
	local flist=$(echo "$flist" | tr ',' ' ')
	for fitem in $flist; do
		# Build the command by replacing all occurrences of '?' in each argument
		local cmd_args=()
		for arg in "$@"; do
			cmd_args+=( "${arg//\?/$fitem}" )
		done
		echo "Running: ${cmd_args[*]}"
		"${cmd_args[@]}"
		sleep 1
	done
}

# detached run
function drun () {
	if [ $# -ne 1 ]; then
		echo "Usage: drun <command>"
		return 1
	fi
	local tmpfile=$(mktemp)
	local cmd="nohup bash -li -c \"$1\" > $tmpfile 2>&1 &"
	# parse args replcae all ? with ;
	cmd="${cmd//\?/;} "
	echo "Running: $cmd"
	eval $cmd
}

function remotePath () {
	if [ $# -ne 1 ]; then
		echo "Usage: remotePath <path>"
		return 1
	fi
	echo "$(whoami)@$(hostname):$(readlink -f "$1")"
}

function nowrap () {
	cut -c-$(tput cols)
}

function calc() {
	bc -l <<< "$*"
}

function mkcd () {
	mkdir -p "$1"
	cd "$1"
}

function diff.dirs {
	local diffout=$(diff -qr $@)
	echo "$diffout" | grep -v "Only in" | grep -v "are identical" | sed 's|Files|vimdiff|' | sed 's|and ||' | sed 's| differ||'
	echo "$diffout" | grep -E "Only in|are identical"
}
