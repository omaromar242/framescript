-- Create ScreenGui and UI elements
local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Create the ScreenGui (this will persist through death)
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = playerGui
screenGui.Enabled = true  -- Ensure the GUI is enabled

-- Create the Frame (Tab)
local tabFrame = Instance.new("Frame")
tabFrame.Size = UDim2.new(0, 200, 0, 400)  -- Increased size for scroll area
tabFrame.Position = UDim2.new(0.5, -100, 0.5, -200)  -- Center the frame
tabFrame.BackgroundColor3 = Color3.fromRGB(128, 0, 128) -- Purple color
tabFrame.Parent = screenGui
tabFrame.ZIndex = 1  -- Set a lower ZIndex for the frame

-- Add TextLabel saying "Made by omar_Gamer"
local madeByLabel = Instance.new("TextLabel")
madeByLabel.Size = UDim2.new(1, 0, 0, 30)  -- Full width of the frame
madeByLabel.Position = UDim2.new(0, 0, 0, 0)  -- Top of the frame
madeByLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0) -- Black background
madeByLabel.TextColor3 = Color3.fromRGB(255, 255, 255) -- White text
madeByLabel.Text = "Made by omar_Gamer"
madeByLabel.Font = Enum.Font.SourceSansBold
madeByLabel.TextSize = 18
madeByLabel.Parent = tabFrame

-- Drag functionality (added to the frame)
local Parent_upvr = tabFrame
local var2_upvw
local var3_upvw
local var4_upvw
local var5_upvw
local TweenService_upvr = game:GetService("TweenService")

local function update_upvr(arg1)
    local var7 = arg1.Position - var4_upvw
    TweenService_upvr:Create(Parent_upvr, TweenInfo.new(0.2, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
        Position = UDim2.new(var5_upvw.X.Scale, var5_upvw.X.Offset + var7.X, var5_upvw.Y.Scale, var5_upvw.Y.Offset + var7.Y);
    }):Play()
end

Parent_upvr.InputBegan:Connect(function(arg1)
    if arg1.UserInputType == Enum.UserInputType.MouseButton1 or arg1.UserInputType == Enum.UserInputType.Touch then
        var2_upvw = true
        var4_upvw = arg1.Position
        var5_upvw = Parent_upvr.Position
        arg1.Changed:Connect(function()
            if arg1.UserInputState == Enum.UserInputState.End then
                var2_upvw = false
            end
        end)
    end
end)

Parent_upvr.InputChanged:Connect(function(arg1)
    if arg1.UserInputType == Enum.UserInputType.MouseMovement or arg1.UserInputType == Enum.UserInputType.Touch then
        var3_upvw = arg1
    end
end)

game:GetService("UserInputService").InputChanged:Connect(function(arg1)
    if arg1 == var3_upvw and var2_upvw then
        update_upvr(arg1)
    end
end)

-- Create Scrolling Frame
local scrollingFrame = Instance.new("ScrollingFrame")
scrollingFrame.Size = UDim2.new(1, 0, 1, -30)  -- Full size of the parent frame minus label height
scrollingFrame.Position = UDim2.new(0, 0, 0, 30) -- Start below the label
scrollingFrame.CanvasSize = UDim2.new(0, 0, 0, 660)  -- Adjusted for additional buttons
scrollingFrame.ScrollBarThickness = 10
scrollingFrame.Parent = tabFrame

-- Function to create a button
local function createButton(name, position, color, parent)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 180, 0, 50)
    button.Position = position
    button.Text = name
    button.BackgroundColor3 = color
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Parent = parent
    return button
end

-- Function to display a notification
local function sendNotification(buttonName)
    game.StarterGui:SetCore("SendNotification", {
        Title = "Button Clicked!";
        Text = "You used: " .. buttonName;
        Duration = 5;
    })
end

-- Existing Buttons
local infYieldButton = createButton("Inf Yield", UDim2.new(0, 10, 0, 30), Color3.fromRGB(255, 0, 0), scrollingFrame)
local espButton = createButton("Esp", UDim2.new(0, 10, 0, 90), Color3.fromRGB(0, 255, 0), scrollingFrame)
local aimlockButton = createButton("Aimlock", UDim2.new(0, 10, 0, 150), Color3.fromRGB(0, 0, 255), scrollingFrame)
local chatLogButton = createButton("ChatLog", UDim2.new(0, 10, 0, 210), Color3.fromRGB(255, 165, 0), scrollingFrame)
local toolGiverButton = createButton("Tool Giver", UDim2.new(0, 10, 0, 270), Color3.fromRGB(255, 255, 0), scrollingFrame)
local teleportPartsButton = createButton("Teleport Parts", UDim2.new(0, 10, 0, 330), Color3.fromRGB(0, 255, 255), scrollingFrame)

-- New Troll Button
local trollButton = createButton("Troll", UDim2.new(0, 10, 0, 390), Color3.fromRGB(128, 0, 128), scrollingFrame)

-- Button Functionalities with Notification
infYieldButton.MouseButton1Click:Connect(function()
    sendNotification("Inf Yield")
    loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source', true))()
end)

espButton.MouseButton1Click:Connect(function()
    sendNotification("Esp")
    loadstring(game:HttpGet("https://raw.githubusercontent.com/omaromar242/Esp/refs/heads/main/Esp"))()
end)

aimlockButton.MouseButton1Click:Connect(function()
    sendNotification("Aimlock")
    loadstring(game:HttpGet("https://raw.githubusercontent.com/omaromar242/aimlock/refs/heads/main/Omarmade"))()
end)

chatLogButton.MouseButton1Click:Connect(function()
    sendNotification("ChatLog")
    loadstring(game:HttpGet("https://raw.githubusercontent.com/omaromar242/chatlog/101d7c6bf69741aa81fe8136e37819cff090f324/Chatlog"))()
end)

toolGiverButton.MouseButton1Click:Connect(function()
    sendNotification("Tool Giver")
    loadstring(game:HttpGet("https://raw.githubusercontent.com/yofriendfromschool1/Sky-Hub-Backup/main/gametoolgiver.lua"))()
end)

teleportPartsButton.MouseButton1Click:Connect(function()
    sendNotification("Teleport Parts")
    loadstring(game:HttpGet("https://raw.githubusercontent.com/Bac0nHck/Scripts/main/BringFlingPlayers"))("More Scripts: t.me/arceusxscripts")()
end)

trollButton.MouseButton1Click:Connect(function()
    sendNotification("Troll")
    loadstring(game:HttpGet("https://raw.githubusercontent.com/yofriendfromschool1/debugnation/main/decompilers%20and%20debugging/Debuggers.txt"))()
end)

-- Toggle frame visibility with the "K" key
local UserInputService = game:GetService("UserInputService")
local frameVisible = true

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    if input.KeyCode == Enum.KeyCode.K then
        frameVisible = not frameVisible
        tabFrame.Visible = frameVisible
    end
end)
