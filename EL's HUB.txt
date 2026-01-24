local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()
local Players = game:GetService("Players")
local Player = Players.LocalPlayer
local Workspace = game:GetService("Workspace")

local Window = Rayfield:CreateWindow({
	Name = "EL's HUB",
	LoadingTitle = "EL's HUB",
	LoadingSubtitle = "Lucky Blocks Game",
	ConfigurationSaving = { Enabled = false }
})

local MainTab  = Window:CreateTab("Main", 4483362458)
local ZonesTab = Window:CreateTab("Zones", 4483362458)
local ShopsTab = Window:CreateTab("Shops", 4483362458)

local Zones = {
	Common     = CFrame.new(-73.6999512, 11, 2.47266769, 1,0,0,0,1,0,0,0,1),
	Uncommon   = CFrame.new(-146.699951, 11, 2.47266769, 1,0,0,0,1,0,0,0,1),
	Rare       = CFrame.new(-226.699951, 11, 2.47266769, 1,0,0,0,1,0,0,0,1),
	Epic       = CFrame.new(-329.699951, 11, 2.47266769, 1,0,0,0,1,0,0,0,1),
	Legendary  = CFrame.new(-465.699951, 11, 2.47266769, 1,0,0,0,1,0,0,0,1),
	Mythic     = CFrame.new(-628.699951, 11, 2.47266769, 1,0,0,0,1,0,0,0,1),
	Divine     = CFrame.new(-983.699951, 11, 2.47266769, 1,0,0,0,1,0,0,0,1),
	Secret     = CFrame.new(-1659.69995, 11, 2.47266769, 1,0,0,0,1,0,0,0,1),
	Cosmic     = CFrame.new(-2149.69995, 11, 2.47266769, 1,0,0,0,1,0,0,0,1)
}

local ZoneOrder = {
	"Common","Uncommon","Rare","Epic","Legendary","Mythic","Divine","Secret","Cosmic"
}

local SelectedZone = ZoneOrder[1]

ZonesTab:CreateDropdown({
	Name = "Select Zone",
	Options = ZoneOrder,
	CurrentOption = { SelectedZone },
	Callback = function(option)
		if type(option) == "table" then
			SelectedZone = option[1]
		else
			SelectedZone = option
		end
	end
})

ZonesTab:CreateButton({
	Name = "Go to Zone",
	Callback = function()
		local hrp = Player.Character and Player.Character:FindFirstChild("HumanoidRootPart")
		if hrp and Zones[SelectedZone] then
			hrp.CFrame = Zones[SelectedZone]
		end
	end
})

MainTab:CreateButton({
	Name = "TP to Safe Zone",
	Callback = function()
		local hrp = Player.Character and Player.Character:FindFirstChild("HumanoidRootPart")
		if hrp then
			hrp.CFrame = CFrame.new(-19.3746128, 18.8950024, 32.7482529, -4.37113883e-08, -1, 0, -4.37113883e-08, 1.91068547e-15, -1, 1, -4.37113883e-08, -4.37113883e-08)
		end
	end
})

MainTab:CreateButton({
	Name = "TP to End",
	Callback = function()
		local hrp = Player.Character and Player.Character:FindFirstChild("HumanoidRootPart")
		if hrp then
			hrp.CFrame = CFrame.new(-2182.5249, 30, 34.149971, 1,0,0,0,1,0,0,0,1)
		end
	end
})

MainTab:CreateButton({
	Name = "Shiftlock (mobile)",
	Callback = function()
		loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Shiftlock-by-namsobased-88371"))()
	end
})

local DisableWaves = false
MainTab:CreateToggle({
	Name = "Disable waves",
	CurrentValue = false,
	Callback = function(v)
		DisableWaves = v
	end
})

task.spawn(function()
	while true do
		if DisableWaves then
			for _, m in ipairs(Workspace:GetChildren()) do
				if m:IsA("Model") and m.Name:match("^WAVE") then
					m:Destroy()
				end
			end
		end
		task.wait(0.4)
	end
end)

local function optimize(obj)
	if obj:IsA("BasePart") then
		obj.Material = Enum.Material.Plastic
		obj.MaterialVariant = nil
		obj.CastShadow = false
	elseif obj:IsA("MeshPart") then
		obj.Material = Enum.Material.Plastic
		obj.TextureID = ""
		obj.MeshId = ""
	elseif obj:IsA("Decal") or obj:IsA("Texture") then
		obj:Destroy()
	end
end

task.spawn(function()
	while true do
		for _, d in ipairs(Workspace:GetDescendants()) do
			optimize(d)
		end
		task.wait(2)
	end
end)

task.spawn(function()
	while true do
		local folder = Workspace:FindFirstChild("LuckyBlockSpawns")
		if folder then
			for _, model in ipairs(folder:GetChildren()) do
				if model:IsA("Model") then
					for _, obj in ipairs(model:GetDescendants()) do
						if obj:IsA("BasePart") then
							if not obj.Name:lower():find("yellow") then
								obj:Destroy()
							else
								obj.Material = Enum.Material.Plastic
								obj.MaterialVariant = nil
							end
						elseif not obj:IsA("Model") then
							obj:Destroy()
						end
					end
				end
			end
		end
		task.wait(1.5)
	end
end)

ShopsTab:CreateButton({
	Name = "Sell all brainrots",
	Callback = function()
		game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.7.0"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("InventoryService"):WaitForChild("RF"):WaitForChild("SellAllBrainrots"):InvokeServer()
		task.wait(0.3)
		Rayfield:Notify({Title = "Success", Content = "All brainrots sold", Duration = 3})
	end
})

ShopsTab:CreateButton({
	Name = "TP to Pickaxe Shop",
	Callback = function()
		local hrp = Player.Character and Player.Character:FindFirstChild("HumanoidRootPart")
		if hrp then
			hrp.CFrame = CFrame.new(-34.35709, 11.2058973, 24.9999695, 1,0,0,0,1,0,0,0,1)
		end
	end
})

ShopsTab:CreateButton({
	Name = "TP to Upgrade Shop",
	Callback = function()
		local hrp = Player.Character and Player.Character:FindFirstChild("HumanoidRootPart")
		if hrp then
			hrp.CFrame = CFrame.new(-34.35709, 11.2058973, 41.9999695, 1,0,0,0,1,0,0,0,1)
		end
	end
})
