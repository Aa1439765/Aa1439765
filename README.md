
local gui = Instance.new("ScreenGui")
gui.Parent = game.Players.LocalPlayer.PlayerGui

local button = Instance.new("TextButton")
button.Text = "Aimbot Başlat"
button.Size = UDim2.new(0, 100, 0, 50)
button.Position = UDim2.new(0, 700, 0, 50)
button.Parent = gui

local aimbotEnabled = false

local function aimbot()
    while aimbotEnabled do
        wait(0.1) -- Aimbot'un ne kadar sık çalışacağını ayarla

        
        local target = nil
        local minAngle = 999 -- Başlangıçta en büyük açıyı ayarla

        
        for _, player in ipairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Team ~= game.Players.LocalPlayer.Team then
                if player.Character and player.Character:FindFirstChild("Head") then
                    local headPosition = player.Character.Head.Position
                    local aimPosition = game.Players.LocalPlayer.Character.Head.Position
                    local angle = (headPosition - aimPosition).magnitude -- Açıyı hesapla
                    if angle < minAngle then
                        minAngle = angle
                        target = headPosition
                    end
                end
            end
        end

        
        if target then
            
            game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid").AutoRotate = false
            local lookVector = (target - game.Players.LocalPlayer.Character.Head.Position).unit
            local newLookAt = CFrame.new(game.Players.LocalPlayer.Character.Head.Position, game.Players.LocalPlayer.Character.Head.Position + lookVector)
            game.Workspace.CurrentCamera.CFrame = newLookAt
        end
    end
end

button.MouseButton1Click:Connect(function()
    aimbotEnabled = not aimbotEnabled -- Aimbot durumunu değiştir

    if aimbotEnabled then
        aimbot() -- Aimbot'u başlat
        button.Text = "Aimbot"
    else
        button.Text = "Aimbot"
    end
end)
