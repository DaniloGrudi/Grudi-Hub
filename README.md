-- Referências aos elementos da UI
local screenGui = script.Parent
local speedTextBox = screenGui:WaitForChild("SpeedTextBox")
local jumpTextBox = screenGui:WaitForChild("JumpTextBox")
local speedButton = screenGui:WaitForChild("SpeedButton")
local jumpButton = screenGui:WaitForChild("JumpButton")
local killButton = screenGui:WaitForChild("KillButton")
local titleLabel = screenGui:WaitForChild("TitleLabel")  -- O título do hub

-- Configurar o título "Grudi Hub"
titleLabel.Text = "Grudi Hub"
titleLabel.TextSize = 36
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255) -- Branco
titleLabel.BackgroundTransparency = 1  -- Deixe o fundo transparente
titleLabel.Position = UDim2.new(0.5, -100, 0, 20)  -- Posicionar o título no topo da tela
titleLabel.AnchorPoint = Vector2.new(0.5, 0)  -- Centralizar o título

-- Função para aumentar a velocidade
local function setSpeed()
    local speed = tonumber(speedTextBox.Text)
    
    if speed and speed > 0 then
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:WaitForChild("Humanoid")
        
        humanoid.WalkSpeed = speed
        print("Velocidade definida para: " .. speed)
    else
        print("Insira um valor válido para a velocidade.")
    end
end

-- Função para aumentar o pulo
local function setJumpHeight()
    local jumpHeight = tonumber(jumpTextBox.Text)
    
    if jumpHeight and jumpHeight > 0 then
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:WaitForChild("Humanoid")
        
        humanoid.JumpHeight = jumpHeight
        print("Altura do pulo definida para: " .. jumpHeight)
    else
        print("Insira um valor válido para a altura do pulo.")
    end
end

-- Função para matar todos os jogadores
local function killAllPlayers()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player.Character then
            local humanoid = player.Character:FindFirstChild("Humanoid")
            if humanoid then
                humanoid.Health = 0
            end
        end
    end
    print("Todos os jogadores foram mortos.")
end

-- Conectar os botões às funções
speedButton.MouseButton1Click:Connect(setSpeed)
jumpButton.MouseButton1Click:Connect(setJumpHeight)
killButton.MouseButton1Click:Connect(killAllPlayers)
