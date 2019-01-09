# IsValidResult

> Reusable code to check if our request was successful.

## Code

Because every response is derived from the same result object, we can use central code to check for errors or warnings
```csharp
private bool IsValidResult(IWS.ExecutionResult response)
{
    //Initialize to true, so no errors
    bool isValid = true;
    if (response.Errors.Length > 0)
    {
        //At least one error, so set to false
        isValid = false;
        //Log all the errors
        foreach (IWS.Error err in response.Errors)
        {
            Log(err.ErrorCode + ": " + err.ErrorCodeExplanation + " (" + err.Field + " - " + err.Value + ")", true);
        }
    }

    //Optionally log all the warnings
    if (response.Warnings.Length > 0)
    {
        //At least one error, so set to false
        isValid = false;
        //Log all the errors
        foreach (IWS.Warning warn in response.Warnings)
        {
            Log(warn.WarningCode + ": " + warn.WarningCodeExplanation + " (" + warn.Field + " - " + warn.Value + ")", true);
        }
    }

    return isValid;
}
```