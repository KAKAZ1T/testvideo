# testvideo
--Abaixo estará Lib da nossa Ui

local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/7yhx/kwargs_Ui_Library/main/source.lua"))()

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Team = LocalPlayer.TeamColor

local UI = Lib:Create{
    Theme = "Dark", -- or any other theme
    Size = UDim2.new(0, 555, 0, 400) -- default
 }
 
 local Main = UI:Tab{
    Name = "Inicio"
 }
 
 local Divider = Main:Divider{
    Name = "Inicio shit"
 }
 
 local QuitDivider = Main:Divider{
    Name = "Sair"
 }

 local KillAll = Divider:Button{
    Name = "ESP",
    Description = "ESP ATIVADO",
    Callback = local function ESP(Player)
        if Player.TeamColor ~= Team then
            local Box = Instance.new("BoxHandleAdornment")
            Box.Size = Player.Character.HumanoidRootPart.Size + Vector3.new(0.1, 0.1, 0.1)
            Box.Adornee = Player.Character.HumanoidRootPart
            Box.AlwaysOnTop = true
            Box.ZIndex = 5
            Box.Transparency = 0.5
            Box.Color3 = Color3.new(1, 0, 0)
            Box.Parent = Player.Character.HumanoidRootPart
        end
    end
 }

 local KillAll = Divider:Button{
    Name = "FOV ESP",
    Description = "FOV ESP ATIVADO!",
    Callback = local function FOV(Player)
        if Player.TeamColor ~= Team then
            local FOV = Instance.new("SelectionBox")
            FOV.LineThickness = 0.05
            FOV.Color3 = Color3.new(1, 0, 0)
            FOV.Transparency = 0.5
            FOV.Adornee = Player.Character.HumanoidRootPart
            FOV.Parent = Player.Character.HumanoidRootPart
        end
    end
    
    local function DisableESP()
        for _, Player in pairs(Players:GetPlayers()) do
            if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
                Player.Character.HumanoidRootPart:FindFirstChildOfClass("BoxHandleAdornment"):Destroy()
            end
        end
    end
    
    local function DisableFOV()
        for _, Player in pairs(Players:GetPlayers()) do
            if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
                Player.Character.HumanoidRootPart:FindFirstChildOfClass("SelectionBox"):Destroy()
            end
        end
    end
    end
 }

 ESP(LocalPlayer)
FOV(LocalPlayer)

Players.PlayerAdded:Connect(function(Player)
    ESP(Player)
    FOV(Player)
end)

Players.PlayerRemoving:Connect(function(Player)
    if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
        Player.Character.HumanoidRootPart:FindFirstChildOfClass("BoxHandleAdornment"):Destroy()
        Player.Character.HumanoidRootPart:FindFirstChildOfClass("SelectionBox"):Destroy()
    end
end)

game:GetService("UserInputService").InputBegan:Connect(function(Input, GameProcessed)
    if Input.KeyCode == Enum.KeyCode.P then
        if ESPEnabled then
            DisableESP()
            DisableFOV()
            ESPEnabled = false
        else
            ESPEnabled = true
        end
    end
end)
