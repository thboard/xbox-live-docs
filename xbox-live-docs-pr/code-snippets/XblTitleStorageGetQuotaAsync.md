```cpp
auto asyncBlock = std::make_unique<XAsyncBlock>();
asyncBlock->queue = queue;
asyncBlock->context = nullptr;
asyncBlock->callback = [](XAsyncBlock* asyncBlock)
{
    std::unique_ptr<XAsyncBlock> asyncBlockPtr{ asyncBlock }; // Take over ownership of the XAsyncBlock*
    size_t usedBytes;
    size_t quotaBytes;
    HRESULT hr = XblTitleStorageGetQuotaResult(asyncBlock, &usedBytes, &quotaBytes);

};

HRESULT hr = XblTitleStorageGetQuotaAsync(
    xboxLiveContext,
    scid,
    storageType,
    asyncBlock.get()
);
if (SUCCEEDED(hr))
{
    // The call succeeded, so release the std::unique_ptr ownership of XAsyncBlock* since the callback will take over ownership.
    // If the call fails, the std::unique_ptr will keep ownership and delete the XAsyncBlock*
    asyncBlock.release();
}
```
