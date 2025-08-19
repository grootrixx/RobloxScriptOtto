local targer = workspace:FindFirstChild("Targer")

--// IK Targer = 
local ikTargets = enemy:FindFirstChild("Ik targets")
local leftFront_IkTarget = ikTargets:FindFirstChild("LeftFront_ikTarger")
local leftBack_IkTarget = ikTargets:FindFirstChild("LeftBack_ikTarger")
local rightFront_IkTarget = ikTargets:FindFirstChild("RightFront_ikTarger")
local rightBack_IkTarget = ikTargets:FindFirstChild("RightBack_ikTarger")

--// Racast parts = 
local raycastParts = enemy:FindFirstChild("RaycastParts")
local leftFront_RaycastPart = raycastParts:FindFirstChild("LeftFront_RaycastPart")
local leftBack_RaycastPart = raycastParts:FindFirstChild("LeftBack_RaycastPart")
local rightFront_RaycastPart = raycastParts:FindFirstChild("RightFront_RaycastPart")
local rightBack_RaycastPart = raycastParts:FindFirstChild("RightsBack_RaycastPart")

--// IKControls
local leftFront_IKControl = hum:FindFirstChild("LeftFront_IKControl")
local leftBack_IKControl = hum:FindFirstChild("LeftBack_IKControl")
local rightFront_IKControl = hum:FindFirstChild("RightFront_IKControl")
local rightBack_IKControl = hum:FindFirstChild("RightBack_IKControl")

leftFront_IKControl.Pole = root.LeftFront_Pole
leftBack_IkTarget.Pole = root.LeftBack_Pole
rightFront_IkTarget.Pole = root.RightFront_Pole
rightBack_IkTarget.Pole = root.RightBack_Pole

--// Модуль 
local ProcedurelModule = require(game:GetService("ReplicatedStorage").ProcedurelModule)

--// RaycastParams
local rayCastParams = RaycastParams.new()
rayCastParams.FilterDescendantsInstances = {enemy}
rayCastParams.FilterType = Enum.RaycastFilterType.Exclude

for _,v: BasePart in ikTargets:GetChildren() do
	v.Transparency = 1 
end

for _,v: BasePart in raycastParts:GetChildren() do
	v.Transparency = 1 
end

coroutine.wrap(function()
	while task.wait(0.25) do 
		hum:MoveTo(target.Position)
	end
end)()

while true do
	ProcedurelModule:IkLegStep(leftFront_IkTarget, leftFront_RaycastPart, enemy.PrimaryPart, 2, 2, 1, 0.05 rayCastParams)
	ProcedurelModule:IkLegStep(rightBack_IkTarget, rightBack_RaycastPart, enemy.PrimaryPart, 2, 2, 1, 0.05 rayCastParams)
	task.wait(0.1)
	ProcedurelModule:IkLegStep(rightFront_IkTarget, rightFront_RaycastPart, enemy.PrimaryPart, 2, 2, 1, 0.05, rayCastParams)
	ProcedurelModule:IkLegStep(leftBack_IkTarget, leftBack_RaycastPart, enemy.PrimaryPart, 2, 2, 1, 0.05, rayCastParams)
	task.wait(0.1)
end
