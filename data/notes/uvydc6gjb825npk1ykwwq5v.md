
## [Set the PATH Environment Variables in Windows PowerShell](https://www.delftstack.com/howto/powershell/set-the-path-environment-variable-in-powershell/)

Other software also relies on the `PATH` environment variable, and accidentally overwriting this may lead to multiple issues. Performing the syntax above will serve as your primary backup for your environment variable values.

To set a new path, you will need to append your new path to the variable by performing a simple string operation.

```powershell
$Env:PATH += ";C:\Program Files\Scripts"
```
