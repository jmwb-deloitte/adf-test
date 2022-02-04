# 🦺 Best practice
https://docs.microsoft.com/en-us/azure/data-factory/source-control

https://docs.microsoft.com/en-us/azure/data-factory/continuous-integration-delivery#best-practices-for-cicd

# 🏗 Interaction Methods
- Data Factory Studio
	| Pro | Con |
	| ----------- | ----------- |
	| Easy to use | Can obscure important info |
	| Fully featured | |
	| Can be used alongside other methods | |
- Azure CLI
	| Pro | Con |
	| ----------- | ----------- |
	| Fast w/ familiarity | Requires manual creation of component JSON files |
	| Automatable | |
	| Can be used alongside other methods | |
- Azure Powershell
	+ Ditto CLI but commands are slightly less legible
- .NET SDK
	+ Calling commands with 10+ parameters that automate REST API calls.
- Python
	+ Ditto .NET SDK
- REST
	+ Ditto Python/.NET but you're calling APIs directly
- ARM Template
	| Pro | Con |
	| ----------- | ----------- |
	| Familiar | Same info as UI |
	| Portable | More confusing than JSON config |

## 🦺 Best Practice
- Develop pipelines in Data Factory Studio, or using software that outputs ARM Templates if more comfortable. This minimizes development time and errors - as all other techniques require correctly formatted API calls and JSON files for each component. This also ensures that changes pass through all quality checks and errors can be debugged and addressed with minimal disruption within these IDEs.
- Small manual modifications should be made either in Data Factory studio, or directly to the JSON files and Data Flow scripts. Ensure git is set up before this to provide version control.
- Automated pipeline creation can be achieved either by:
	+ (ideally) Utilising environment variables to have pipelines use dynamic information as part of their processing without building new pipelines. (e.g. have a main pipeline that dynamically configures and runs secondary pipelines)
	+ Building a template pipeline, which is then automatically **modified** by the solutions that interact with the API (not recommended as this results in a lot of regex heavy code which can be very sensitive to change and require a lot of upkeep)

# ⛓Git Interaction
- Create a github repo (needs to be public) or a (premium) microsoft CI/CD Studio(??)
- Adds "Save" functionality to data factory studio, which automatically *commits and pushes changes*.

## 🦺 Best Practice
Data Factory should **always** be connected to a feature and dev branch, **never** a live branch. Additionally, developers should always develop new features on feature branches and then merge to avoid conflicts.
- This should be paired with a **CI/CD pipeline** to ensure contributions are properly tested before deployment to a live environment - as it's easier than ever for changes to unintentionally make their way into final dev builds.
