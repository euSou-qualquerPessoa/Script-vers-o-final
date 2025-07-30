local player = game.Players.LocalPlayer
local UIS = game:GetService("UserInputService")

-- GUI principal
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "UltimateGui"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = game.CoreGui

-- Botão de alternar menu
local ToggleButton = Instance.new("TextButton")
ToggleButton.Parent = ScreenGui
ToggleButton.Size = UDim2.new(0, 80, 0, 30)
ToggleButton.Position = UDim2.new(0, 10, 0.05, 0)
ToggleButton.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Text = "Menu"
ToggleButton.Font = Enum.Font.SourceSansBold
ToggleButton.TextSize = 20

-- Frame do menu
local MenuFrame = Instance.new("Frame")
MenuFrame.Parent = ScreenGui
MenuFrame.Size = UDim2.new(0, 140, 0, 170)
MenuFrame.Position = UDim2.new(0, 10, 0.12, 0)
MenuFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MenuFrame.BorderSizePixel = 0
MenuFrame.Visible = true

-- Abrir/fechar menu
ToggleButton.MouseButton1Click:Connect(function()
    MenuFrame.Visible = not MenuFrame.Visible
end)

-- Botão TP
local TPButton = Instance.new("TextButton")
TPButton.Parent = MenuFrame
TPButton.Size = UDim2.new(1, -10, 0, 30)
TPButton.Position = UDim2.new(0, 5, 0, 5)
TPButton.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
TPButton.TextColor3 = Color3.fromRGB(255, 255, 255)
TPButton.Text = "TP"
TPButton.Font = Enum.Font.SourceSansBold
TPButton.TextSize = 20

TPButton.MouseButton1Click:Connect(function()
    local Tool = Instance.new("Tool")
    Tool.Name = "tpUser"
    Tool.RequiresHandle = false
    Tool.CanBeDropped = false

    Tool.Activated:Connect(function()
        local mouse = player:GetMouse()
        local connection
        connection = mouse.Button1Down:Connect(function()
            if mouse.Hit then
                player.Character:MoveTo(mouse.Hit.Position)
            end
            connection:Disconnect()
        end)
    end)

    Tool.Parent = player.Backpack
end)

-- Botão Velocidade
local SpeedButton = Instance.new("TextButton")
SpeedButton.Parent = MenuFrame
SpeedButton.Size = UDim2.new(1, -10, 0, 30)
SpeedButton.Position = UDim2.new(0, 5, 0, 40)
SpeedButton.BackgroundColor3 = Color3.fromRGB(255, 170, 0)
SpeedButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SpeedButton.Text = "Velocidade"
SpeedButton.Font = Enum.Font.SourceSansBold
SpeedButton.TextSize = 18

-- Botão Infinite Jump (label)
local JumpLabel = Instance.new("TextLabel")
JumpLabel.Parent = MenuFrame
JumpLabel.Size = UDim2.new(1, -10, 0, 25)
JumpLabel.Position = UDim2.new(0, 5, 0, 75)
JumpLabel.BackgroundColor3 = Color3.fromRGB(0, 200, 127)
JumpLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
JumpLabel.Text = "🪂 Infinite Jump: ON"
JumpLabel.Font = Enum.Font.SourceSansBold
JumpLabel.TextSize = 16

-- Botão Hitbox
local HitboxButton = Instance.new("TextButton")
HitboxButton.Parent = MenuFrame
HitboxButton.Size = UDim2.new(1, -10, 0, 25)
HitboxButton.Position = UDim2.new(0, 5, 0, 105)
HitboxButton.BackgroundColor3 = Color3.fromRGB(170, 0, 170)
HitboxButton.TextColor3 = Color3.fromRGB(255, 255, 255)
HitboxButton.Text = "Hitbox: OFF"
HitboxButton.Font = Enum.Font.SourceSansBold
HitboxButton.TextSize = 16

-- Painel Velocidade
local SpeedFrame = Instance.new("Frame")
SpeedFrame.Parent = ScreenGui
SpeedFrame.Size = UDim2.new(0, 140, 0, 210)
SpeedFrame.Position = UDim2.new(0, 160, 0.12, 0)
SpeedFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
SpeedFrame.Visible = false

SpeedButton.MouseButton1Click:Connect(function()
    SpeedFrame.Visible = not SpeedFrame.Visible
end)

local SpeedTitle = Instance.new("TextLabel")
SpeedTitle.Parent = SpeedFrame
SpeedTitle.Size = UDim2.new(1, 0, 0, 30)
SpeedTitle.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
SpeedTitle.Text = "Escolha a velocidade"
SpeedTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
SpeedTitle.Font = Enum.Font.SourceSansBold
SpeedTitle.TextSize = 18

local function createSpeedButton(text, value, y)
    local btn = Instance.new("TextButton")
    btn.Parent = SpeedFrame
    btn.Size = UDim2.new(1, -10, 0, 30)
    btn.Position = UDim2.new(0, 5, 0, y)
    btn.BackgroundColor3 = Color3.fromRGB(0, 170, 127)
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Text = text
    btn.Font = Enum.Font.SourceSansBold
    btn.TextSize = 20

    btn.MouseButton1Click:Connect(function()
        local char = player.Character
        if char and char:FindFirstChildOfClass("Humanoid") then
            char:FindFirstChildOfClass("Humanoid").WalkSpeed = value
        end
    end)
end

createSpeedButton("Padrão (16)", 16, 40)
createSpeedButton("Rápido (50)", 50, 75)
createSpeedButton("Insano (100)", 100, 110)

local SpeedBox = Instance.new("TextBox")
SpeedBox.Parent = SpeedFrame
SpeedBox.Size = UDim2.new(1, -10, 0, 30)
SpeedBox.Position = UDim2.new(0, 5, 0, 145)
SpeedBox.BackgroundColor3 = Color3.fromRGB(90, 90, 90)
SpeedBox.TextColor3 = Color3.fromRGB(255, 255, 255)
SpeedBox.PlaceholderText = "Digite valor"
SpeedBox.Font = Enum.Font.SourceSans
SpeedBox.TextSize = 18
SpeedBox.ClearTextOnFocus = false

local ApplySpeed = Instance.new("TextButton")
ApplySpeed.Parent = SpeedFrame
ApplySpeed.Size = UDim2.new(1, -10, 0, 30)
ApplySpeed.Position = UDim2.new(0, 5, 0, 180)
ApplySpeed.BackgroundColor3 = Color3.fromRGB(0, 120, 255)
ApplySpeed.TextColor3 = Color3.fromRGB(255, 255, 255)
ApplySpeed.Text = "Aplicar"
ApplySpeed.Font = Enum.Font.SourceSansBold
ApplySpeed.TextSize = 20

ApplySpeed.MouseButton1Click:Connect(function()
    local speed = tonumber(SpeedBox.Text)
    if speed and speed > 0 then
        local char = player.Character
        if char and char:FindFirstChildOfClass("Humanoid") then
            char:FindFirstChildOfClass("Humanoid").WalkSpeed = speed
        end
    else
        SpeedBox.Text = ""
        SpeedBox.PlaceholderText = "Valor inválido"
    end
end)

-- Infinite Jump
UIS.JumpRequest:Connect(function()
    local char = player.Character
    if char and char:FindFirstChildOfClass("Humanoid") then
        char:FindFirstChildOfClass("Humanoid"):ChangeState(Enum.HumanoidStateType.Jumping)
    end
end)

-- /tp NomeDoJogador via chat
player.Chatted:Connect(function(msg)
    local prefix = "/tp "
    if msg:sub(1, #prefix):lower() == prefix then
        local targetName = msg:sub(#prefix + 1):lower()
        for _, plr in pairs(game.Players:GetPlayers()) do
            if plr ~= player and plr.Name:lower():sub(1, #targetName) == targetName then
                local char = plr.Character
                if char and char:FindFirstChild("HumanoidRootPart") then
                    player.Character:MoveTo(char.HumanoidRootPart.Position + Vector3.new(0, 3, 0))
                end
                return
            end
        end
    end
end)

-- Hitbox ativar/desativar
local hitboxAtiva = false
local function aplicarHitbox(plr)
    if plr.Character and plr ~= player then
        for _, part in pairs(plr.Character:GetChildren()) do
            if part:IsA("Part") or part:IsA("MeshPart") then
                if hitboxAtiva then
                    part.Size = Vector3.new(5, 5, 5)
                    part.Transparency = 0.5
                    part.Material = Enum.Material.ForceField
                    part.CanCollide = false
                else
                    part.Size = Vector3.new(2, 2, 1)
                    part.Transparency = 0
                    part.Material = Enum.Material.Plastic
                end
            end
        end
    end
end

HitboxButton.MouseButton1Click:Connect(function()
    hitboxAtiva = not hitboxAtiva
    HitboxButton.Text = "Hitbox: " .. (hitboxAtiva and "ON" or "OFF")
    for _, plr in pairs(game.Players:GetPlayers()) do
        if plr ~= player then
            aplicarHitbox(plr)
        end
    end
end)

game.Players.PlayerAdded:Connect(function(plr)
    plr.CharacterAdded:Connect(function()
        wait(1)
        aplicarHitbox(plr)
    end)
end)
