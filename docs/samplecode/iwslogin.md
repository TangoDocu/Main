<!-- docs/op/loginblock.md -->
# IWSLogin()

> The login block is part of every web service operation and takes care of the authentication before executing the web service.

## Struture
See [full explanation](/op/loginblock.md)

## Example code
Because the login block logic is needed for every web service operation, it can be interesting to put this in a reusable function
```csharp
        private IWS.Login IWSLogin()
        {
            IWS.Login login_Block = new IWS.Login()
            {
                Dispatcher = varUser,
                Password = varPwd,
                Language = "EN",
                Integrator = varInt,
                SystemNr = Convert.ToInt32(varCustId)
            };

            return login_Block;

        }
``` 