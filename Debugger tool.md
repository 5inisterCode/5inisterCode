-- My Debugger tool
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()
local Window = OrionLib:MakeWindow({Name = "Debugger Tool", Icon = "rbxassetid://4483345998", HidePremium = false, IntroEnabled = false , SaveConfig = false , ConfigFolder = "OrionTest"})

local Bypass = Window:MakeTab({
    Name = "Bypass Tools",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})
Bypass:AddButton({
    Name = "Bypass Adonis Newindex Anticheat",
	Callback = function()
		local players = game:GetService('Players')
		local lplr = players.LocalPlayer
		local lastCF, stop, heartbeatConnection
		local function start()
			heartbeatConnection = game:GetService('RunService').Heartbeat:Connect(function()
				if stop then
					return 
				end 
				lastCF = lplr.Character:FindFirstChildOfClass('Humanoid').RootPart.CFrame
			end)
			lplr.Character:FindFirstChildOfClass('Humanoid').RootPart:GetPropertyChangedSignal('CFrame'):Connect(function()
				stop = true
				lplr.Character:FindFirstChildOfClass('Humanoid').RootPart.CFrame = lastCF
				game:GetService('RunService').Heartbeat:Wait()
				stop = false
			end)    
			lplr.Character:FindFirstChildOfClass('Humanoid').Died:Connect(function()
				heartbeatConnection:Disconnect()
			end)
		end

		lplr.CharacterAdded:Connect(function(character)
			repeat 
				game:GetService('RunService').Heartbeat:Wait() 
			until character:FindFirstChildOfClass('Humanoid')
			repeat 
				game:GetService('RunService').Heartbeat:Wait() 
			until character:FindFirstChildOfClass('Humanoid').RootPart
			start()
		end)

		lplr.CharacterRemoving:Connect(function()
			heartbeatConnection:Disconnect()
		end)

		start()

	end
})
Bypass:AddButton({
    Name = "Bypass Anti Kick",
    Callback = function()
        local mt = getrawmetatable(game)

        setreadonly(mt, false)

        local oldmt = mt.__namecall

        mt.__namecall = newcclosure(function(Self, ...)


        local method = getnamecallmethod()

        if method == 'Kick' then
        
            print("Tried To kick")
            wait(9e9)
            return nil

        end

        return oldmt(Self, ...)

        end)

        setreadonly(mt, true)
        print("Anti Kick Bypassed")
    end
})

Bypass:AddButton({
    Name = "Anti AFK",
    Callback = function()
        local vu = game:GetService("VirtualUser")
        game:GetService("Players").LocalPlayer.Idled:Connect(function()
            vu:Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
            wait(1)
            vu:Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
        end)
        print("Anti AFK Bypassed")
    end
})

Bypass:AddButton({
    Name = "Adonis Bypass",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/Pixeluted/adoniscries/main/Source.lua'))()
        print("Adonis Bypassed")
    end
})

--Debugger Tools
local Debugger = Window:MakeTab({
    Name = "Debugger Tools",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

Debugger:AddButton({
    Name = "Infinite Yield",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/edgeiy/infiniteyield/master/source'))()
    end    
})
Debugger:AddButton({
    Name = "Dark Dex Infinite Yield",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/infyiff/backup/main/dex.lua"))()
    end
})
Debugger:AddButton({
    Name = "Dark Dex V3",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/Cynacol/Dark-Dex-V3/refs/heads/main/Dark%20Dex%20V3.txt'))()
    end  
})
Debugger:AddButton({
    Name = "Dark Dex V4",
    Callback = function()
        loadstring(game:HttpGet('https://gist.githubusercontent.com/dannythehacker/1781582ab545302f2b34afc4ec53e811/raw/ee5324771f017073fc30e640323ac2a9b3bfc550/dark%2520dex%2520v4'))()
    end
})
Debugger:AddButton({
    Name = "SimpleSpy",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/Pixeluted/adoniscries/main/Source.lua'))()
        print("Adonis Bypassed")
        loadstring(game:HttpGet('https://raw.githubusercontent.com/exxtremestuffs/SimpleSpySource/refs/heads/master/SimpleSpy.lua'))()
    end    
})

Debugger:AddButton({
    Name = "Turtle Spy",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/Pixeluted/adoniscries/main/Source.lua'))()
        print("Adonis Bypassed")
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Turtle-Brand/Turtle-Spy/main/source.lua", true))()
    end    
})

Debugger:AddButton({
    Name = "Hydroxide",
    Callback = function()
        local owner = "Upbolt"
        local branch = "revision"
        local function webImport(file)
            return loadstring(game:HttpGetAsync(("https://raw.githubusercontent.com/%s/Hydroxide/%s/%s.lua"):format(owner, branch, file)), file .. '.lua')()
        end
        webImport("init")
        webImport("ui/main")
    end
})

Debugger:AddButton({
	Name = "Console Log",
	Callback = function()
        game:GetService("VirtualInputManager"):SendKeyEvent(true, Enum.KeyCode.F9, false, game)
        game:GetService("VirtualInputManager"):SendKeyEvent(false, Enum.KeyCode.F9, false, game)
	end    
})

-- HiddenTools
local HiddenTools = Window:MakeTab({
	Name = "HiddenTools",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

HiddenTools:AddButton({
    Name = "Game UI/Frame Viewer",
    Callback = function()
        loadstring(game:HttpGet("https://gist.githubusercontent.com/iHereSin/a489384a98010932427c160550494a9f/raw/8957bea8215509ed020d5010a1e60114cb87e029/Hidden%2520UI%2520Giver"))()
    end
})
HiddenTools:AddButton({
	Name = "Game Tool Giver",
	Callback = function()
		loadstring(game:HttpGet("https://gist.githubusercontent.com/iHereSin/eadb35c4e4f657947159f7cd1d4fb40a/raw/d55fcacbfd29a5f74793a89c11a71b8a3e04cddf/ToolGiver"))()
	end    
})

HiddenTools:AddButton({
    Name = "Game Tool Equipper",
    Callback = function()
        loadstring(game:HttpGet("https://gist.githubusercontent.com/iHereSin/dbdf66c9d215d8b41aa48122f0d8b92f/raw/f956afc0915c60c22407b8b3a84362f115ad139d/Game%2520Tool"))()
    end    
})

-- Server Tools
local Server = Window:MakeTab({
    Name = "Server Tool Info",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local Players = game:GetService("Players")
local TeleportService = game:GetService("TeleportService")
local PlaceId = game.PlaceId
local JobId = game.JobId
local GameName = game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId).Name

Server:AddButton({
    Name = "Game Name :  "..GameName,
    Callback = function()
        setclipboard(GameName)
    end
})

Server:AddButton({
    Name = "JobId :  "..game.JobId,
    Callback = function()
        local jobId = game.JobId
        setclipboard(jobId)
    end    
})
Server:AddButton({
    Name = "PlaceId :  "..game.PlaceId,
    Callback = function()
        local placeId = game.PlaceId
        setclipboard(placeId)
    end    
})

Server:AddButton({
    Name = "Server Hop",
    Callback = function()
        local servers = game:GetService("TeleportService"):GetGameServers(game.PlaceId)
        for i,v in pairs(servers) do
            game:GetService("TeleportService"):TeleportToPlaceInstance(game.PlaceId, v.id)
        end
    end    
})

Server:AddButton({
    Name = "Rejoin",
    Callback = function()
        if #Players:GetPlayers() <= 1 then
            Players.LocalPlayer:Kick("\nRejoining...")
            wait()
            TeleportService:Teleport(PlaceId, Players.LocalPlayer)
        else
            TeleportService:TeleportToPlaceInstance(PlaceId, JobId, Players.LocalPlayer)
        end
    end    
})




OrionLib:Init()
