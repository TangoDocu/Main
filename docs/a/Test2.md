# Test2

> The Wabco - Transics web services library for full integration with all your fleet data


```csharp
 		private void SetTripAndPlaceFlagsBasedonSettingValue(VehicleMappingFlags flags)
        {
            var includePlanningSetting = CurrentCustomer.CustomerIntegrationSettings.IWSIncludePlanningForVehicles;
            if(includePlanningSetting == 0) 
			//Hier houdt men enkel rekening met de waarde 0, terwijl de generic setting niet bestaat en dus NULL is. Vandaar dat de plannings informatie in alle web services nog doorkomt. Hier moet men ook controleren op NULL
            {
                flags.IncludeCurrentTrip = false;
                flags.IncludeLastPlace = false;
            }
        }
        private void SetTripAndPlaceFlagsBasedonSettingValue(VehicleMappingFlags flags, bool includePlanning = false)
        {
            var includePlanningSetting = CurrentCustomer.CustomerIntegrationSettings.IWSIncludePlanningForVehicles;
            switch(includePlanningSetting)
            {
                case 0:
                case null: 
				//Hier houdt men rekening met NULL en 0, de generic setting bestaat niet en kan niet aangemaakt worden, dus altijd 0, de includePlanning vlag wordt dus altijd genegeerd. Dit mag volgens mij zo blijven.
                        flags.IncludeCurrentTrip = false;
                        flags.IncludeLastPlace = false;                
                    break;
                case 1:
                    if(!includePlanning)
                    {
                        flags.IncludeCurrentTrip = false;
                        flags.IncludeLastPlace = false;
                    }
                    break;
                default:
                    break;
            }
        }
```