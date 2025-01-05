-- Função para desenhar linhas e exibir nomes dos jogadores
local function drawESP(player)
    -- Criar uma linha conectando o jogador a outro jogador
    local playerPos = player.Character.HumanoidRootPart.Position
    local myPos = game.Players.LocalPlayer.Character.HumanoidRootPart.Position

    -- Criar a linha
    local line = Instance.new("Part")
    line.Size = Vector3.new(0.1, 0.1, (playerPos - myPos).magnitude)
    line.CFrame = CFrame.new((playerPos + myPos) / 2, playerPos)
    line.Anchored = true
    line.CanCollide = false
    line.BrickColor = BrickColor.new("White")
    line.Material = Enum.Material.SmoothPlastic
    line.Parent = workspace

    -- Criar uma caixa de texto para exibir o nome do jogador
    local billboardGui = Instance.new("BillboardGui")
    billboardGui.Adornee = player.Character.Head
    billboardGui.Size = UDim2.new(0, 100, 0, 50)
    billboardGui.StudsOffset = Vector3.new(0, 3, 0)
    billboardGui.Parent = player.Character.Head

    local nameLabel = Instance.new("TextLabel")
    nameLabel.Text = player.Name
    nameLabel.Size = UDim2.new(1, 0, 1, 0)
    nameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    nameLabel.BackgroundTransparency = 1
    nameLabel.TextScaled = true
    nameLabel.Parent = billboardGui
end

-- Função para checar jogadores próximos
local function checkPlayers()
    while true do
        wait(0.5)  -- Checa a cada meio segundo
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                drawESP(player)
            end
        end
    end
end

-- Iniciar a verificação dos jogadores
checkPlayers()
