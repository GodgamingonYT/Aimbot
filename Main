local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local Workspace = game:GetService("Workspace")
local CoreGui = game:GetService("CoreGui")

local player = Players.LocalPlayer
local camera = Workspace.CurrentCamera

-- Settings
local Settings = {
    -- Aimbot Settings
    AimbotEnabled = false,
    AimbotMode = "Nearest", -- "Nearest" or "Center"
    LerpFactor = 0.2, -- Smoothness (0.1 = snappy, 0.5 = smooth)
    CheckInterval = 0.01, -- Target check frequency (seconds)

    -- Outline Settings
    OutlineFillColor = Color3.fromRGB(255, 0, 0), -- Red fill (transparent)
    OutlineColor = Color3.fromRGB(255, 0, 0), -- Red outline
    OutlineFillTransparency = 1, -- No fill
    OutlineTransparency = 0.5, -- Visible outline

    -- UI Settings
    MainFrameSize = UDim2.new(0, 128, 0, 136), -- Tight fit, 16px padding
    MainFramePosition = UDim2.new(0.5, -64, 0.5, -68),
    MainFrameColor = Color3.fromRGB(25, 25, 30),
    TitleBarSize = UDim2.new(1, 0, 0, 24),
    TitleBarColor = Color3.fromRGB(30, 30, 35),
    ContentFrameColor = Color3.fromRGB(30, 30, 35), -- Contrast
    ContentFrameSize = UDim2.new(1, 0, 0, 112), -- 136 - 24
    ButtonSize = UDim2.new(0, 96, 0, 32), -- Original size
    ToggleButtonPosition = UDim2.new(0.5, -48, 0, 16),
    ModeButtonPosition = UDim2.new(0.5, -48, 0, 64), -- 16px gap
    MinimizeButtonSize = UDim2.new(0, 24, 0, 24),
    MinimizeButtonPosition = UDim2.new(1, -48, 0, 0),
    MinimizeButtonColor = Color3.fromRGB(40, 40, 45),
    CloseButtonSize = UDim2.new(0, 24, 0, 24),
    CloseButtonPosition = UDim2.new(1, -24, 0, 0),
    CloseButtonColor = Color3.fromRGB(140, 50, 50),
    ButtonOffColor = Color3.fromRGB(140, 50, 50),
    ButtonOnColor = Color3.fromRGB(70, 130, 70),
    ModeButtonColor = Color3.fromRGB(50, 50, 140), -- Blue
    TextColor = Color3.fromRGB(255, 255, 255),
    CloseButtonTextColor = Color3.fromRGB(255, 220, 220),
    CornerRadius = UDim.new(0, 12),
    TitleTextSize = 14,
    ButtonTextSize = 12,
    MinimizeTextSize = 16,
}

-- Randomize Name Function
local function generateRandomName()
    local chars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
    local name = ""
    for _ = 1, 32 do
        name = name .. chars:sub(math.random(1, #chars), math.random(1, #chars))
    end
    return name
end

-- UI Setup
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = generateRandomName()
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = CoreGui

local MainFrame = Instance.new("Frame")
MainFrame.Name = generateRandomName()
MainFrame.Size = Settings.MainFrameSize
MainFrame.Position = Settings.MainFramePosition
MainFrame.BackgroundColor3 = Settings.MainFrameColor
MainFrame.BorderSizePixel = 0
MainFrame.Visible = true
MainFrame.Parent = ScreenGui

local UICorner = Instance.new("UICorner")
UICorner.Name = generateRandomName()
UICorner.CornerRadius = Settings.CornerRadius
UICorner.Parent = MainFrame

local TitleBar = Instance.new("Frame")
TitleBar.Name = generateRandomName()
TitleBar.Size = Settings.TitleBarSize
TitleBar.BackgroundColor3 = Settings.TitleBarColor
TitleBar.BorderSizePixel = 0
TitleBar.Visible = true
TitleBar.Parent = MainFrame

local TitleCorner = Instance.new("UICorner")
TitleCorner.Name = generateRandomName()
TitleCorner.CornerRadius = Settings.CornerRadius
TitleCorner.Parent = TitleBar

local Title = Instance.new("TextLabel")
Title.Name = generateRandomName()
Title.Size = UDim2.new(0.7, 0, 1, 0)
Title.BackgroundTransparency = 1
Title.Text = "Aimbot"
Title.TextColor3 = Settings.TextColor
Title.TextSize = Settings.TitleTextSize
Title.Font = Enum.Font.GothamBold
Title.Visible = true
Title.Parent = TitleBar

local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Name = generateRandomName()
MinimizeButton.Size = Settings.MinimizeButtonSize
MinimizeButton.Position = Settings.MinimizeButtonPosition
MinimizeButton.BackgroundColor3 = Settings.MinimizeButtonColor
MinimizeButton.Text = "−"
MinimizeButton.TextColor3 = Settings.TextColor
MinimizeButton.TextSize = Settings.MinimizeTextSize
MinimizeButton.Font = Enum.Font.GothamBold
MinimizeButton.Visible = true
MinimizeButton.Parent = TitleBar

local MinimizeCorner = Instance.new("UICorner")
MinimizeCorner.Name = generateRandomName()
MinimizeCorner.CornerRadius = Settings.CornerRadius
MinimizeCorner.Parent = MinimizeButton

local CloseButton = Instance.new("TextButton")
CloseButton.Name = generateRandomName()
CloseButton.Size = Settings.CloseButtonSize
CloseButton.Position = Settings.CloseButtonPosition
CloseButton.BackgroundColor3 = Settings.CloseButtonColor
CloseButton.Text = "X"
CloseButton.TextColor3 = Settings.CloseButtonTextColor
CloseButton.TextSize = Settings.MinimizeTextSize
CloseButton.Font = Enum.Font.GothamBold
CloseButton.Visible = true
CloseButton.Parent = TitleBar

local CloseCorner = Instance.new("UICorner")
CloseCorner.Name = generateRandomName()
CloseCorner.CornerRadius = Settings.CornerRadius
CloseCorner.Parent = CloseButton

local ContentFrame = Instance.new("Frame")
ContentFrame.Name = generateRandomName()
ContentFrame.Size = Settings.ContentFrameSize
ContentFrame.Position = UDim2.new(0, 0, 0, 24)
ContentFrame.BackgroundColor3 = Settings.ContentFrameColor
ContentFrame.BorderSizePixel = 0
ContentFrame.Visible = true
ContentFrame.Parent = MainFrame

local ContentCorner = Instance.new("UICorner")
ContentCorner.Name = generateRandomName()
ContentCorner.CornerRadius = Settings.CornerRadius
ContentCorner.Parent = ContentFrame

local ToggleButton = Instance.new("TextButton")
ToggleButton.Name = generateRandomName()
ToggleButton.Size = Settings.ButtonSize
ToggleButton.Position = Settings.ToggleButtonPosition
ToggleButton.BackgroundColor3 = Settings.ButtonOffColor
ToggleButton.Text = "Aimbot: OFF"
ToggleButton.TextColor3 = Settings.TextColor
ToggleButton.TextSize = Settings.ButtonTextSize
ToggleButton.Font = Enum.Font.GothamBold
ToggleButton.Visible = true
ToggleButton.Parent = ContentFrame

local ToggleCorner = Instance.new("UICorner")
ToggleCorner.Name = generateRandomName()
ToggleCorner.CornerRadius = Settings.CornerRadius
ToggleCorner.Parent = ToggleButton

local ModeButton = Instance.new("TextButton")
ModeButton.Name = generateRandomName()
ModeButton.Size = Settings.ButtonSize
ModeButton.Position = Settings.ModeButtonPosition
ModeButton.BackgroundColor3 = Settings.ModeButtonColor
ModeButton.Text = "Mode: Nearest"
ModeButton.TextColor3 = Settings.TextColor
ModeButton.TextSize = Settings.ButtonTextSize
ModeButton.Font = Enum.Font.GothamBold
ModeButton.Visible = true
ModeButton.Parent = ContentFrame

local ModeCorner = Instance.new("UICorner")
ModeCorner.Name = generateRandomName()
ModeCorner.CornerRadius = Settings.CornerRadius
ModeCorner.Parent = ModeButton

-- UI Functionality
local minimized = false
local tweenInfo = TweenInfo.new(0.2, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)

MinimizeButton.MouseButton1Click:Connect(function()
    if minimized then
        local tween = TweenService:Create(MainFrame, tweenInfo, {Size = Settings.MainFrameSize})
        tween:Play()
        tween.Completed:Wait()
        MinimizeButton.Text = "−"
        ContentFrame.Visible = true
        minimized = false
    else
        local tween = TweenService:Create(MainFrame, tweenInfo, {Size = UDim2.new(0, 128, 0, 24)})
        ContentFrame.Visible = false
        tween:Play()
        tween.Completed:Wait()
        MinimizeButton.Text = "+"
        minimized = true
    end
end)

CloseButton.MouseButton1Click:Connect(function()
    local tween = TweenService:Create(MainFrame, tweenInfo, {
        Size = UDim2.new(0, 128, 0, 0),
        BackgroundTransparency = 1
    })
    tween:Play()
    for _, child in pairs(MainFrame:GetDescendants()) do
        if child:IsA("GuiObject") then
            if child:IsA("TextLabel") or child:IsA("TextButton") then
                TweenService:Create(child, tweenInfo, {TextTransparency = 1, BackgroundTransparency = 1}):Play()
            elseif child:IsA("Frame") then
                TweenService:Create(child, tweenInfo, {BackgroundTransparency = 1}):Play()
            end
        end
    end
    tween.Completed:Wait()
    ScreenGui:Destroy()
end)

-- Draggable GUI
local dragging, dragInput, dragStart, startPos
TitleBar.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = MainFrame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

TitleBar.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

-- Aimbot Logic
local currentTarget = nil
local currentHighlight = nil

local function getChar(plr)
    return plr.Character
end

local function isAlive(humanoid)
    return humanoid and humanoid.Health > 0
end

local function isSameTeam(targetPlayer)
    if not player.Team or not targetPlayer.Team then
        return false -- Assume different teams if undefined
    end
    return player.Team == targetPlayer.Team
end

local function updateHighlight(targetHead)
    if currentHighlight then
        currentHighlight:Destroy()
        currentHighlight = nil
    end
    if targetHead and Settings.AimbotEnabled then
        local targetChar = targetHead.Parent
        if targetChar and targetChar:IsA("Model") then
            currentHighlight = Instance.new("Highlight")
            currentHighlight.Name = generateRandomName()
            currentHighlight.FillColor = Settings.OutlineFillColor
            currentHighlight.OutlineColor = Settings.OutlineColor
            currentHighlight.FillTransparency = Settings.OutlineFillTransparency
            currentHighlight.OutlineTransparency = Settings.OutlineTransparency
            currentHighlight.Adornee = targetChar
            currentHighlight.Parent = targetChar
        end
    end
end

local function findNearestTarget()
    local char = getChar(player)
    local localPlayerRoot = char and char:FindFirstChild("HumanoidRootPart")
    if not localPlayerRoot then return nil end
    local localPlayerPosition = localPlayerRoot.Position

    local closestTarget = nil
    local closestDistance = math.huge

    for _, targetPlayer in pairs(Players:GetPlayers()) do
        if targetPlayer ~= player and not isSameTeam(targetPlayer) then
            local targetChar = getChar(targetPlayer)
            local humanoid = targetChar and targetChar:FindFirstChild("Humanoid")
            local head = targetChar and targetChar:FindFirstChild("Head")
            if humanoid and head and isAlive(humanoid) then
                local distance = (head.Position - localPlayerPosition).Magnitude
                if distance < closestDistance then
                    closestDistance = distance
                    closestTarget = head
                end
            end
        end
    end
    return closestTarget
end

local function findCenterTarget()
    local char = getChar(player)
    if not char then return nil end

    local closestTarget = nil
    local closestScreenDistance = math.huge
    local screenCenter = Vector2.new(camera.ViewportSize.X / 2, camera.ViewportSize.Y / 2)

    for _, targetPlayer in pairs(Players:GetPlayers()) do
        if targetPlayer ~= player and not isSameTeam(targetPlayer) then
            local targetChar = getChar(targetPlayer)
            local humanoid = targetChar and targetChar:FindFirstChild("Humanoid")
            local head = targetChar and targetChar:FindFirstChild("Head")
            if humanoid and head and isAlive(humanoid) then
                local screenPoint, onScreen = camera:WorldToViewportPoint(head.Position)
                if onScreen then
                    local screenPos = Vector2.new(screenPoint.X, screenPoint.Y)
                    local distance = (screenPos - screenCenter).Magnitude
                    if distance < closestScreenDistance then
                        closestScreenDistance = distance
                        closestTarget = head
                    end
                end
            end
        end
    end
    return closestTarget
end

-- Mode Switching
local function toggleMode()
    if Settings.AimbotMode == "Nearest" then
        Settings.AimbotMode = "Center"
        ModeButton.Text = "Mode: Center"
    else
        Settings.AimbotMode = "Nearest"
        ModeButton.Text = "Mode: Nearest"
    end
    if Settings.AimbotEnabled then
        currentTarget = Settings.AimbotMode == "Nearest" and findNearestTarget() or findCenterTarget()
        updateHighlight(currentTarget)
    end
end

ModeButton.MouseButton1Click:Connect(toggleMode)

-- Aimbot Toggle
local function toggleAimbot()
    Settings.AimbotEnabled = not Settings.AimbotEnabled
    if Settings.AimbotEnabled then
        ToggleButton.Text = "Aimbot: ON"
        ToggleButton.BackgroundColor3 = Settings.ButtonOnColor
        currentTarget = Settings.AimbotMode == "Nearest" and findNearestTarget() or findCenterTarget()
        updateHighlight(currentTarget)
    else
        ToggleButton.Text = "Aimbot: OFF"
        ToggleButton.BackgroundColor3 = Settings.ButtonOffColor
        currentTarget = nil
        updateHighlight(nil)
    end
end

ToggleButton.MouseButton1Click:Connect(toggleAimbot)

-- Keybind
UserInputService.InputBegan:Connect(function(input, gameProcessedEvent)
    if gameProcessedEvent then return end
    if input.KeyCode == Enum.KeyCode.T then
        toggleAimbot()
    end
end)

-- Target Update Loop
spawn(function()
    while true do
        if Settings.AimbotEnabled then
            currentTarget = Settings.AimbotMode == "Nearest" and findNearestTarget() or findCenterTarget()
            updateHighlight(currentTarget)
        else
            currentTarget = nil
            updateHighlight(nil)
        end
        task.wait(Settings.CheckInterval) -- ~100Hz
    end
end)

-- Camera Aiming Loop
RunService.RenderStepped:Connect(function()
    if Settings.AimbotEnabled and currentTarget then
        local targetPos = currentTarget.Position
        local currentCFrame = camera.CFrame
        local targetCFrame = CFrame.new(currentCFrame.Position, targetPos)
        camera.CFrame = currentCFrame:Lerp(targetCFrame, Settings.LerpFactor)
    end
end)
