
https://levelup.gitconnected.com/5-modern-bash-scripting-techniques-that-only-a-few-programmers-know-4abb58ddadad

# Displaying Animations to Indicate Long-Running Tasks

```bash
#!/bin/bash
sleep 5 &
pid=$!
frames="/ | \\ -"
while kill -0 $pid 2&>1 > /dev/null;
do
    for frame in $frames;
    do
        printf "\r$frame Loading..."
        sleep 0.5
    done
done
printf "\n"
```

# Displaying Native GUI Notifications from Bash

GNU/Linux-based operating systems

```bash
#!/bin/bash
sleep 10
notify-send "notify.sh" "Task #1 was completed successfully"
```

macOS users can execute the [AppleScript](https://en.wikipedia.org/wiki/AppleScript) interpreter from Bash to display native notifications as follows:

```bash
#!/bin/bash
sleep 10
osascript -e "display notification \"Task #1 was completed successfully\" with title \"notify.sh\""
```

# Multiprocessing in Bash Scripts

```bash
#!/bin/bash
function task1() {
    echo "Running task1..."
    sleep 5
}
function task2() {
    echo "Running task2..."
    sleep 5
}
task1 &
task2 &
wait
echo "All done!"
```

# Displaying GUI components with Bash

# Modernizing the Terminal Output with Text Styles
