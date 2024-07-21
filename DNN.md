# DNN

```python
from torch.utils.data import Dataset, DataLoader
import torch.nn as nn

class MyDataset(Dataset):
    def __init__(self, file):
        self.data = ...
    def __getitem__(self, index):
        return self.data[index]
    def __len__(self):
        return len(self.data)

dataset = MyDataset(file)
dataloader = DataLoader(dataset, batch_size, shuffle=True) ## shuffle when training

class MyModel(nn.Module):
    def __init__(self):
        super(MyModel, self).__init__()
        self.net = nn.Sequential(
        	nn.Linear(10, 32),
            nn.Sigmoid(),
            nn.Linear(32, 1)
        )
        
    def forward(self, x):
        return self.net(x)
 
## preprocess
dataset = MyDataset(file)
tr_set = DataLoader(dataset, 16, shuffle=True)
model = MyModel.to(device)
criterion = nn.MSELoss()
optimizer = torch.optim.SGD(model.parameters(), 0.1)

##train
for epoch in range(n_epochs):
    model.train()
    for x, y in tr_set:
        optimizer.zero_grad()
        x, y = x.to(device), y.to(device)
        pred = model(x)
        loss = criterion(pred, y)
        loss.backward()
        optimizer.step()

## validation
model.eval()
total_loss = 0
for x, y in dv_set:
    x, y = x.to(device), y.to(device)
    with torch.no_grad():
        pred = model(x)
        loss = criterion(pred, y)
    total_loss += loss.cpu().item() * len(x)
avg_loss = total_loss / len(dv_set.dataset)

##testing
model.eval()
preds = []
for x in tt_set:
    x = x.to(device)
    with torch.no_grad():
        pred = model(x)
        preds.append(pred.cpu)
        
## Save
torch.save(model.state_dict(), path)

## Load
ckpt = torch.load(path)
model.load_state_dict(ckpt)
```

