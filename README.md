-- Script Auto Đánh Có Menu GUI
-- Dán vào executor (Synapse X, Hydrogen, Fluxus...)

-- Tạo GUI
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local ToggleButton = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui
ScreenGui.Name = "AutoClickGui"

Frame.Size = UDim2.new(0, 150, 0, 50)
Frame.Position = UDim2.new(0, 20, 0, 100)
Frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Frame.Parent = ScreenGui

ToggleButton.Size = UDim2.new(1, 0, 1, 0)
ToggleButton.Text = "BẬT AUTO ĐÁNH"
ToggleButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Parent = Frame

-- Auto Click Biến
local autoClick = false
local VirtualInputManager = game:GetService("VirtualInputManager")
local RunService = game:GetService("RunService")

-- Kết nối nút bật/tắt
ToggleButton.MouseButton1Click:Connect(function()
    autoClick = not autoClick
    ToggleButton.Text = autoClick and "TẮT AUTO ĐÁNH" or "BẬT AUTO ĐÁNH"
end)

-- Vòng lặp auto click
RunService.RenderStepped:Connect(function()
    if autoClick then
        VirtualInputManager:SendMouseButtonEvent(0, 0, 0, true, game, 0)
        VirtualInputManager:SendMouseButtonEvent(0, 0, 0, false, game, 0)
    end
end)
