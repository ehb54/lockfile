# lockfile #

Package lockfile implements a simple automatic lockfile (PID) method for golang.

## Updates to Fork parent

This version checks for a command line match to the pid if the pid is running.
This is useful after a system reboot when another process may have taken the PID.

## Usage

    import "github.com/ehb54/lockfile"

### Example
```go
    if lock, err := lockfile.Lock(filename); err != nil {
        panic(err)
    } else {
        defer lock.Unlock()
    }
```

### Reference

#### func  Lock

```go
func Lock(name string) (*LockFile, error)
```
Lock automatically checks if the file already exists, if so, reads the process
ID from the file and checks if the process is running. If the process is running
a nil lock is returned and an error stating "Locked by other process".

#### func (*LockFile) Unlock

```go
func (l *LockFile) Unlock()
```
Unlock closes and deletes the lock file previously created by Lock()

#### func  ProcessRunning

```go
func ProcessRunning(pid int) bool
```
ProcessRunning is a cross-platform check to work on both Windows and Unix
systems as the os.FindProcess() function works differently.
