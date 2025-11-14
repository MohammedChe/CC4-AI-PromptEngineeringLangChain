# Setup Troubleshooting Guide

## Issues You Encountered

### 1. PowerShell Execution Policy Error
**Error:** 
```
cannot be loaded because running scripts is disabled on this system
```

**Solution:**
Run this command ONCE in PowerShell (as Administrator):
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Then activate the virtual environment with:
```powershell
. .\.venv\Scripts\Activate.ps1
```

### 2. pyzmq Build Error (ModuleNotFoundError: No module named 'pipes')
**Error:**
```
ModuleNotFoundError: No module named 'pipes'
```

**Cause:** 
The `pipes` module was removed in Python 3.13. Your requirements specified `pyzmq==22.2.1`, which is incompatible with Python 3.13+.

**Solution (ALREADY APPLIED):**
Updated `requirements.txt`:
- Changed `pyzmq==22.2.1` → `pyzmq==26.0.3`

This version is fully compatible with Python 3.13+.

### 3. Linux Command in PowerShell
**Error:**
```
source : The term 'source' is not recognized as a cmdlet
```

**Cause:** 
`source` is a bash/Linux command, not PowerShell.

**Solutions:**

**Option A - PowerShell (Native):**
```powershell
. .\.venv\Scripts\Activate.ps1
```

**Option B - Git Bash:**
```bash
source ./.venv/Scripts/activate
```

## Next Steps

1. **Activate your virtual environment** (choose one based on your shell):
   - PowerShell: `. .\.venv\Scripts\Activate.ps1`
   - Git Bash: `source ./.venv/Scripts/activate`

2. **Verify the installation is complete** by checking:
   ```
   pip list | grep pyzmq
   ```
   You should see `pyzmq 26.0.3` or similar.

3. **Install any missing LangChain packages** (if needed):
   ```
   pip install langchain-openai langchain-huggingface langchain-core
   ```

4. **Test in Jupyter Notebook:**
   Start your notebook and run the cells to verify everything works.

## Python Version Info

To check your Python version:
```
python --version
```

If you're using Python 3.13+, always ensure packages are compatible with that version.
