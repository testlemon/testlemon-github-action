# TestLemon official GitHub Action

GitHub Action for TestLemon runner.

# Usage

```yml
name: Pipeline

on:
  workflow_dispatch:

jobs:
  test:
    runs-on: 'ubuntu-latest'
    
    steps:
    - name: Code checkout
      uses: actions/checkout@v4

    - name: Run TestLemon
      uses: itbusina/testlemon-action@v0.2
      with:
          image: itbusina/testlemon:latest
          input_dir: ./tests
          output_dir: ./output
          network: container:serverundertest
          args: |
            --collections ./tests/colection.json \
            --parallel \
            --variables host=https://serverundertest:8080 \
            --output output \
            --license ${{ secrets.APIBEELICENSE }}

    - name: Archive output results
      if: always()
      uses: actions/upload-artifact@v4
      with:
        name: report
        path: ./output/
```

## License

Testlemon is licensed under the Apache License, Version 2.0. View a copy of the [License file](https://github.com/testlemon/testlemon-core/blob/main/LICENSE).